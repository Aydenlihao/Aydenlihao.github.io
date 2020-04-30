---
title: 数组的push、unshift、pop、shift方法实现
date: 2020-04-30 11:06:15
tags:
  - 数组
category: JavaScript
---

## 尾部添加(push)

`push()函数将一个或者多个元素添加到数组的末尾，并返回该数组的新长度`
从解释中可以看出，push 函数只要将要添加的元素依次放到数组的最后即可，不会改变原有数组元素的索引。所以循环参数列表，将新元素依次放到数组的最后即可。

```javascript
Array.prototype._push = function (...value) {
  for (var i = 0; i < arguments.length; i++) {
    this[this.length] = arguments[i];
  }
  return this.length;
};
var arr = [1, 2, 3, 4];
arr._push(9, 8);
console.log(arr); // [ 1, 2, 3, 4, 9, 8 ]
```

## 头部添加(unshift)

`unshift()函数将将一个或者多个元素添加到数组的开头，并返回该数组的新长度（该函数修改原有数组）`
向数组的头部添加元素，数组的长度也会发生变化，但不像尾部添加的操作，数组原有元素索引不改变。做头部添加的操作，需要将原有元素的索引向左移动。
例如只添加一位，则需要将数组的每个元素的索引依次向右移一位，假设原来数组长度是 4，头部添加一个元素，长度变为 5。所以现在就变成：**array.length = 5**,而目前**array[5-1]**是最后一个元素，现在由于依次往后移动，所以，**array[5-1]必须是最后一个元素**
**所以我们可以从数组的最后一位的下一位往前循环，将 array[i]赋值为 array[i-1]**循环到 1 停，将 array 的第 0 项赋值为需要添加的值。
过程如下
![](/images/array/unshift.png)
具体代码实现：

```javascript
Array.prototype._unshift = function(value) { for (let i = this.length; i > 0; i--) {
 this[i] = this[i - 1] } this[0] = value return this.length
}
var arr = [1, 2, 3, 4];
arr._unshift(8);
console.log(arr); // [ 8, 1, 2, 3, 4 ]
```

## 尾部删除 (pop)

`pop()函数将删除arrayObject的最后一个元素，把数组长度减1，并且返回它删除的元素的值，如果数组已经为空，则pop()不改变数组，并返回undefined值`

## 头部删除（shift）

`shift()函数用于把数组的第一个元素从其中删除，并返回第一个元素的值`
