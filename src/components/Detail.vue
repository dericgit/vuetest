<template>
<div class="summary-page">
  <div v-html="summary" class="summary">{{summary}}</div>
  <div v-html="image" class="summary-img">{{image}}</div>
</div>
</template>
<script>
export default {
  props: ['description'],
  data () {
    return {
      desc: this.description.__cdata,
      summary: null,
      image: null
    }
  },
  created () {
    const reg = /<p>[\s\S]*?<\/p>/gi
    const removeTag = /<(?:.|\s)*?>/g
    let page = this.desc.match(reg)
    let img = this.desc.match(/<img[^>]+\/>/gi)
    let summary = page[1]
    for (var i = 1; i < page.length; i++) {
      if (page[i].replace(removeTag, '')) {
        summary = page[i].replace(removeTag, '')
        break
      }
    }
    this.summary = summary
    if (img && img[0]) {
      this.image = img[0]
    }
  }
}
</script>
<style>
.summary-page {
  overflow: hidden;
}
.summary {
  float: left;
  text-indent: 12px;
  font-size: 12px;
  color: #666;
  overflow: hidden;
  width: 70%;
}
.summary-img {
  position: relative;
  float: right;
  width: 100px;
  height: 100px;
  overflow: hidden;
}
.summary-img img {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 50%;
  transform: translate(-50%, -50%);
}
</style>
