<template>
  <div class="rss-container" @scroll="onScroll($event)">
    <div class="rss-version">{{version}} {{description}} {{title}}</div>
    <div class="rss-list">
      <div class="list-item" v-for="(item,idx) in tenItem">
        <h1 class="p-title">
          <a :href="item.link">{{item.title.__cdata}}</a>
        </h1>
        <div class="p-cate">
          <strong>{{item.author}}</strong>
          <span>{{item.category}}</span>
          <label>{{item.pubDate.__cdata}}</label>
        </div>
        <detail :description="item.description"></detail>
      </div>
      <div class="list-loading" v-if="needLoad">加载中...</div>
    </div>
  </div>
</template>

<script>
// x2js  ''
import data from '../store/36kr.json'
import Detail from '../components/Detail'

export default {
  name: 'hello',
  data () {
    return {
      listData: data.rss,
      page: 1,
      pageSize: 10,
      needLoad: false
    }
  },
  computed: {
    version () {
      return this.listData._version
    },
    kr () {
      return this.listData.channel
    },
    description () {
      return this.kr.description
    },
    generator () {
      return this.kr.generator
    },
    lists () {
      return this.kr.item
    },
    language () {
      return this.kr.language
    },
    link () {
      return this.kr.link
    },
    pubData () {
      return this.kr.pubDate
    },
    title () {
      return this.kr.title
    },
    tenItem () {
      const total = this.page * this.pageSize - 1
      return this.lists.slice(0, total)
    }
  },
  created () {
    console.log(this.listData)
  },
  methods: {
    onScroll (event) {
      const offsetHeight = event.currentTarget.offsetHeight
      const scrollHeight = event.target.scrollHeight
      const scrollTop = event.target.scrollTop
      const scrollBottom = offsetHeight + scrollTop
      if (scrollBottom === scrollHeight || scrollBottom === scrollHeight + 2) {
        if (this.page >= Math.ceil(this.lists.length / this.pageSize)) {
          return
        }
        this.needLoad = true
        setTimeout(() => {
          this.page++
          this.needLoad = false
        }, 2000)
      }
    }
  },
  components: {
    Detail
  }
}
</script>

<style scoped>
.rss-container {
  position: relative;
  height: 100%;
  width: 100%;
  overflow-y: scroll;
}
.rss-version {
  display: none;
}
.list-item {
  padding-bottom: 15px;
  border-bottom: 1px solid #ccc;
  margin-bottom: 30px;
}
.p-title {
  font-size: 16px;
}
.p-cate {
  margin-bottom: 10px;
  font-size: 12px;
  color: #999;
}
.p-cate strong {
  padding: 2px 8px;
  background: #ccc;
  border-radius: 5px;
}
.p-cate span {}
.p-cate label {
  float: right;
}
.list-loading {
  text-align: center;
}
</style>
