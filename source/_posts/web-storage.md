---
title: web-storage
date: 2016-06-12 18:37:06
tags: html5
---

## 写在开始

HTML4 中可以使用 cookie 在客户端保存诸如用户名等简单信息，但是实际使用中，我们发现 cookie 存储永久数据存在以下问题：

- 大小：cookie 的大小被限制在 4kb。
- 带宽：cookie 是跟随 HTTP 事务一起被发送的，因此会浪费一部分发送 cookie 时使用的带宽。
- 复杂性：操作 cookie 的方法需要自己封装。

针对 cookie 存储存在的这些问题，HTML5 提供了三种本地存储方式，分别是 Web Storage、Web SQL Database 和 IndexDB。本篇主要整理记录应用最为广泛的是 Web Storage。

## 简述

Web Storage 存储类似于object的键值对。其中，键 (key) 可以是strings或者integers，而值 (value) 只能是strings。所以数据写入的时候都会隐式调用toString方法转成字符串。

Web Storage 分为两种：

- **sessionStorage** 将数据存储在 session 对象中。 所谓 session , 是指用户在浏览某网页时，从进入网页到窗口关闭所经过的时间。

	sessionStorage 是在同源同窗口中始终存在的数据，也就是只要该浏览器窗口没有关闭，即使在该窗口中刷新当前页面或者打开同源的另一页面，数据依然存在。关闭窗口后，sessionStorage 就会被销毁。同时独立打开不同的窗口，即使是同一页面，sessionStorage 对象也不相同。
	
- **localStorage** 将数据保存在客户端本地的硬件设备中。sessionStorage 类似，最大的区别是生命周期不同，即使浏览器关闭也会持久保存在本地，除非手动清除。有同源同浏览器的限制。

## 浏览器兼容

到目前为止，IE8 以上、Firefox3.6 以上、Chrome6 以上、Safari5 以上、Opera10.50 以上版本浏览器均支持 web storage 。
 

## 可存放数据大小

一般浏览器中，每个域名下的 localStorage、sessionStorage 均可以存储5MB大小的数据。

## 判断浏览器是否支持

在使用 Web Storage 之前有必要检测当前浏览器是否支持。 接下来已 localStorage 为例。

若当前浏览器支持 localStorage，则 window 对象上存在 localStorage 属性，然而仅仅判读 localStorage 属性的存在性是不够的，有些浏览器虽然能够找到 localStorage，但是此 localStorage 却不是 available 的。综上，需要两步来检测是否支持：

~~~javascript
function storageAvailable (type) {
  try {
    var storage = window[type]
    var str = '__storage_test__'
    storage.setItem(str, str)
    storage.removeItem(str)
    return true
  }
  catch(e) {
    return false
  }
}
~~~

接下来可以使用了：

~~~javascript
if (storageAvailable('localStorage')) {
  // use localStorage here
} else {
  // some warning or error msg here
}
~~~

## 基本操作
以下均已 window.localStorage 为例：

1. 获取数据

	~~~javascript
	var data = localStorage.getItem('data') // getItem 可以从 storage 中获取数据项，接受数据项的key作为参数，返回数据值value
	var data = localStorage['data']
	var data = localStorage.data // 注意data是字符串
	~~~

2. 存储数据

	~~~javascript
	localStorage.setItem('data', data) // setItem 可以用来创建新的数据项或者更新已存在的值。接受要创建/修改的数据项的 key 和对应的 value
	localStorage['data'] = data
	localStorage.data = data
	~~~

3. 删除记录

	~~~javascript
	localStorage.removeItem('data') // 根据传入的 key 移除数据项
	localStorage.clear() // 不接收参数，直接清空整个存储对象
	~~~
	
## storage 事件

修改 web storage 中的值时会触发 window 对象的 storage 事件。需要注意的是，重复设置相同的键值不会触发该事件，在同一个页面内发生的变化不会触发该事件，在相同域名下的其他页面中修改时才会触发。

注：对于 sessionStorage, 只有相互牵连的窗口改动sessionStorage的时候才会触发

对于 localStorage, 如果浏览器两个标签页都打开了来自同源的页面，其中一个页面修改了 localStorage, 另外一个页面将收到 storage 事件。


事件对象有如下属性：

	event.key // 在 web storage 中被修改的数据键值。
	event.oldValue // 在 web storage 中被修改前的值。
	event.newValue // 在 web storage 中被修改后的值。
	event.url // 修改 web storage 中值的页面的 url 地址。
	event.storageArea // 被变动的 sessionStorage 对象 或 localStorage 对象。

一个栗子：

~~~javascript
window.addEventListener('storage', function(e){
  document.querySelector('.my-key').textContent = e.key
  document.querySelector('.my-old').textContent = e.oldValue
  document.querySelector('.my-new').textContent = e.newValue
  document.querySelector('.my-url').textContent = e.url
  document.querySelector('.my-storage').textContent = e.storageArea
})
~~~

## 使用场景及安全性考虑

一些需要长时间保存的 webapp 的本地缓存可以使用 localStorage 进行保存。有些内容较多的表单填写为了优化用户体验会将单页面拆分成多个子页面，引导用户一步一步去填写，这个时候可以使用 sessionStorage 存储中间内容。 

由于在浏览器开发者模式下可以对 sessionStorage 和 localStorage 随意读取和修改，所以尽量不要存储敏感信息，对已存储的内容进行提交时进行安全校验。
