# HTML5新特性

- 新增语义化标签：<footer>、<article>、<nav>、<section>、<header>等。
- 用于绘画的<canvas>标签。
- 用于媒体回放的<video>和<audio>标签。
- 存储：提供了sessionStorage和localStorage。
- 新增input类型：color、url、email、date、datetimelocal等。
- 新增表单控件：placeholder、autofocus、autocomlpete等。

## canvas标签

只是一个二维网格的图形容器，绘制图形要用js来定位绘制。

比如画一条线，要先找到canvas元素，创建context对象，用moveTo和lineTo定位，再用stroke绘制。

```
var c=document.getElementById("myCanvas"); 
var ctx=c.getContext("2d"); 
ctx.moveTo(0,0); 
ctx.lineTo(200,100); 
ctx.stroke();
```

再比如画圆，也要先找到canvas元素，创建context对象，用beginPath开始路径，用arc确定圆的位置和大小，然后closePath关闭路径，最后再用stroke或fill绘制。

```
var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.beginPath();
ctx.arc(95,50,40,0,2*Math.PI);
ctx.closePath();
ctx.stroke();
```

## canvas(基于js)

- 依赖分辨率
- 不支持事件处理器
- 弱的文本渲染能力
- 能够以 .png 或 .jpg 格式保存结果图像
- 最适合图像密集型的游戏，其中的许多对象会被频繁重绘

## svg(基于xml)

- 不依赖分辨率
- 支持事件处理器
- 最适合带有大型渲染区域的应用程序（比如谷歌地图）
- 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
- 不适合游戏应用