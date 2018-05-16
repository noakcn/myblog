---
title: jquery 事件冒泡
date: 2017-3-31 10:49:58
tags:
- javascript
- html
categories:
- 笔记
---

首先可以来看一个例子：

```html
<div id="dOne" onclick="alert('我是最外层')">
   <div id="dTwo" onclick="alert('我是中间层')">
     <a href="http://www.baidu.com" id="aTree" onclick="alert('我是最里层')">click me</a>
   </div>
</div>
```
[点击运行](https://jsfiddle.net/noakcn/4hjh4957/7/)

上面这个示例分3层：`dOne` 最外面一层，`dTwo`中间层，`a`标签在最里层，他们各自有自己的`onclick`事件。

运行后会发现一次弹出`我是最里层-->我是中间层-->我是最外层`然后跳转到百度。

那么为什么会这样呢？

<!-- more -->

这个就要讲讲jquery的事件冒泡了。

> 在一个对象上触发某类事件（比如单击事件），如果此对象定义了处理此事件的处理程序，那么此事件就会调用这个处理程序，如果没有定义出此事件的处理程序或者事件返回true，那么这个事件就会向这个对象的父级对象传播，从里到外，直至他被处理，或者到达对象层次的最顶层，即document对象（有些是window)

**然而有时候这并不是我们所需要的,那该如何处理呢？**

我们可以阻止事件的冒泡行为。

1. event.stopPropagation(); 

```javascript
$(function() {
  $("#aTree").click(function(e) {
    e.stopPropagation();
  })
})
```

[点击运行](https://jsfiddle.net/noakcn/4hjh4957/4/)

这时候就会发现只有 `我是最里层`被执行，然后跳转至百度，达到了阻止事件往外冒泡。

2. return false

```javascript
$(function() {
  $("#aTree").click(function(e) {
    return false;
  })
})
```

[点击运行](https://jsfiddle.net/noakcn/4hjh4957/5/)

也是只有 `我是最里层`被执行，虽然阻止了事件往外冒泡，但是却不跳转百度。

3. event.preventDefault();

```javascript
$(function() {
  $("#aTree").click(function(e) {
    e.preventDefault();
  })
})
```

[点击运行](https://jsfiddle.net/noakcn/4hjh4957/6/)

运行后依次出现`我是最里层-->我是中间层-->我是最外层` 但是不跳转百度

### 总结

1. event.stopPropagation();

事件处理过程中，阻止了事件的冒泡，不会阻止默认行为。

2. return false;

事件处理过程中，阻止了事件的冒泡，但是也阻止了默认行为。

3. event.preventDefault();

事件处理过程中，不阻止冒泡，但是阻止默认行为。