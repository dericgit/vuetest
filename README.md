### test
**1.** 有一个长度未知的数组a，如果它的长度为0就把数字1添加到数组里面，否则按照先进先出的队列规则让第一个元素出队
```
const a = [1, 2, 3, 4, 5];
function specifyArr(arr) {
	if (a.length === 0) {
		a.push(1);
	} else {
		a.shift();	
	}
}
specifyArr(a);
```
**2.** console.log('hello'.repeatify(3))
    
   期望打印出hellohellohello
```
String.prototype.repeatify = function(n) {
	let result = '';
	if (n > 1) {
		for (let i = 0; i < n; i++) {
			result += this;
		}
	} else {
		result = this;
	}
	return result;
};
console.log('Hello'.repeatify(3));
```
**3.** 下面代码如何改可以让person()打印出Colin Ihrig

```javascript

	var fullname = 'John Doe'
	var obj = {
		fullname: 'Colin Ihrig',
		getFullname: function() {
		return this.fullname
		}
	}
	 	 
	var person = obj.getFullname
	console.log(obj.getFullname()) // Colin Ihrig
	console.log(person()) // John Doe
	
```
```
console.log(person.call(obj))
```

**4.** 不使用loop循环，创建一个长度为100的数组，并且每个元素的值等于它的下标
```
function createArrWidthLen (n, arr) {
	if (n > 0) {
		arr[n-1] = n - 1;
		return createArrWidthLen(n-1, arr);
	}
}
const arr = [];
createArrWidthLen(100, arr);
console.log(arr, arr.length);
```