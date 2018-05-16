---
title: HTML 5 Canvas 
date: 2017-3-31 10:32:16
tags: 
- html5
- canvas
- h5
categories:
- 笔记
---

```html
<canvas id="myCanvas" width="200" height="100" style="border:1px solid #000000;"></canvas>
```

[点击运行](https://jsfiddle.net/noakcn/fzyttzso/4/)

> `<canvas></canvas>`创建一个画布

**<canvas>**本身没有绘图功能，需要搭配JavaScript来绘图

```javascript
var c = document.getElementById("myCanvas");//首先，找到<canvas>元素
var ctx = c.getContext("2d");//创建context对象
ctx.fillStyle = "#FF0000";//颜色
ctx.fillRect(0, 0, 150, 75); //大小 fillRect(x,y,width,height) 
```

[点击运行](https://jsfiddle.net/noakcn/fzyttzso/2/)

<!-- more -->

**Canvas坐标**

![](http://om8bq99t5.bkt.clouddn.com/17-3-28/94347096-file_1490683818919_afa9.png)

> canvas 的左上角坐标为 (0,0) 


**Canvas - 路径**

绘制一条斜线

```javascript
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
ctx.moveTo(0,0); //moveTo(x,y) 定义线条开始坐标
ctx.lineTo(200,100);//lineTo(x,y) 定义线条结束坐标
ctx.stroke();//实际地绘制出通过 moveTo() 和 lineTo() 方法定义的路径。
```

[点击运行](https://jsfiddle.net/noakcn/fzyttzso/3/)

绘制一个圆

```javascript
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
ctx.beginPath();
ctx.arc(95,50,40,0,2*Math.PI);//arc(x,y,r,start,stop)
ctx.stroke();
```

[点击运行](https://jsfiddle.net/noakcn/fzyttzso/5/)



**Canvas - 文本 **

```javascript
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
ctx.font="30px Arial"; //定义字体
ctx.fillText("Hello World",10,50);//绘制实心文字 fillText(text,x,y) 
```

[点击运行](https://jsfiddle.net/noakcn/fzyttzso/6/)

```javascript
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
ctx.font="30px Arial";
ctx.strokeText("Hello World",10,50);
```

[点击运行](https://jsfiddle.net/noakcn/fzyttzso/7/)

**Canvas - 渐变**

线条渐变

```javascript
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
//创建渐变
var grd = ctx.createLinearGradient(0,0,200,0);//createLinearGradient(x,y,x1,y1) - 创建线条渐变
grd.addColorStop(0,"red");
grd.addColorStop(1,"white");

//填充渐变
ctx.fillStyle = grd;
ctx.fillRect(10,10,150,80);
```

[点击运行](https://jsfiddle.net/noakcn/fzyttzso/8/)

径向/圆渐变

```javascript
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
//创建渐变
var grd = ctx.createRadialGradient(75,50,5,90,60,100);//createRadialGradient(x,y,r,x1,y1,r1) - 创建一个径向/圆渐变
grd.addColorStop(0,"red");
grd.addColorStop(1,"white");

//填充渐变
ctx.fillStyle = grd;
ctx.fillRect(10,10,150,80);
```



**Canvas - 图像**

把一副图像放置到画布上

```html
<img width="220" height="277" src="http://om8bq99t5.bkt.clouddn.com/17-3-30/35361084-file_1490843381323_5aa4.png" alt="图像" id="scream">
<canvas id="myCanvas" width="250" height="300" style="border:1px solid #000000;"></canvas>
```

```javascript
var c = document.getElementById("myCanvas");
var ctx = c.getContext("2d");
var img = document.getElementById("scream");
ctx.drawImage(img,10,10); //绘图
```

[点击运行](https://jsfiddle.net/noakcn/fzyttzso/10/)

