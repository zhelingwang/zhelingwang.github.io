---
title: CSS常用知识
tags: ['CSS','interview']
id: css
categories: CSS
---
# CSS

## 1.什么是标签语义化

```text
合理的标签做合适的事情
```

## 2.有哪些标签？

### 1.标签分类与区别

```text
1.分类
    块级标签：div , p , ul , ol , li , h1~h6,header,footer,section,main
    行内标签：a span small i em strong
    行内块级标签：img,input

2.区别 
    1.独占一行与否
    2.宽高设置，默认宽度是容器100%还是本身的宽度
    3.水平垂直方向上的内外边际；

	block : 独占一行；宽高可设置，默认宽度是容器的100%；水平和垂直方向的内外边距均可设置；
	inline ：与其它行内元素或行内块元素共占一行，但中间会有空白的间隙；宽高不可设置，默认宽度是自身内容宽度；只能设置水平方向上的内外边距；
	inline-block : 和相邻的行内元素（行内块）在一行上，中间也会有空隙；宽高，内边距和外边距都可以设置，默认宽度是本身内容的宽度；
	
3.如何转换？
    display:block inline inline-block
```

<!-- more -->

### 2.display其它值

```
display 还有哪些值？ 
1.none
如何让元素隐藏？ 
display:none / visibility:hidden，二者有什么区别？是否占据文档流
opacity，IE678不兼容如何处理？
	可以用 filter ,那filter除了设置透明度还能做什么？还能设置滤镜，模糊度和反色 
2.flex
	项目中何时用到flex？居中和响应式
	除了flex还有什么可以居中？
		父容器设置同高度的line-height;
		定位和负的margin(已知宽高)，translate(-50%，-50%)(未知宽高);
	响应式布局还有哪些？rem/media/width百分比
	都有哪些盒子模型？border-box,content-box
3.table
```
## 3.盒子水平垂直居中方案
```js
五大方案：
1、2.三种定位
	1.absolute + top/left:50% + margin-top/left: -宽高一半的显式数值
	2.absolute + top/left/right/bottom:0 + margin:auto (隐式数值但必须有宽高)
	3.absolute + top/left:50% + transform: translate(-50%,-50%); 
		(无需指明宽高也可以，有兼容问题)
	
3.display:flex , 移动端经常用，有兼容
	.container{
		display:flex;
		justify-content:center;
		align-items:center;
	}

4.javascript
    <div class="box" id="box">box</div> // id 可以直接作为 DOM 元素对象
	let HTML = document.documentElement,
                winW = HTML.clientWidth,
                winH = HTML.clientHeight,
                boxW = box.offsetWidth,
                boxH = box.offsetHeight;
	box.style.position = "absolute";
	box.style.left = (winW - boxW) / 2 + 'px';
	box.style.top = (winH - boxH) / 2 + 'px';
	
5. display:table-cell 很少用
    .father{	
        display:table-cell;
        vertical-align:middle;
        text-align:center;
    }
//1.父容器必须有固定宽高,不能是百分比
//2.table-cell原用于文本居中的，故子元素需加 display:inline-block/inline
```

## 4.盒模型

```
1.标准盒模型 box-sizing:content-box
2.怪异(IE)盒模型 box-sizing:border-box
3.flex弹性盒模型
4.多列布局盒模型 常用于pad文本阅读器，多列布局，基本不用
```

## 5.几大经典布局方案

```
实现左右固定，中间自适应的布局
1.圣杯布局
	原理：结构，container > (center+left+right),container padding-left/right 预留出左右两端的宽度,再把左右两块区域移动到预留区域，可使用 浮动 + 负margin 或 position 来完成。
2.双飞翼布局
	原理：结构，container>center + left + right ，center的margin-left/right预留出左右两端的宽度,再把左右两块区域移动到预留区域，可使用 浮动 + 负margin 或 position 来完成。
3.CALC,尽可能别在css中使用表达式，执行慢且兼容性差
	.center{
		width:calc(100%-400px);
		min-height:400px;
		background:red;
	}
4.flex
5.定位
```
### 1.圣杯布局

```css
第一种：left/center/right
html,body {height: 100%;overflow: hidden;}
.container {height: 100%;padding: 0 200px;  /* 因为left/right的width：200px */}
.left,.right{width: 200px;min-height: 200px;background-color: royalblue;}
.left,.center,.right {float: left;}
.center {width: 100%;min-height: 400px;background: lightsalmon;}
.left{margin-left: -200px;}
.right{margin-right: -200px;}
<div class="container">
    <div class="left"></div>
    <div class="center"></div>
    <div class="right"></div>
</div>

第二种：center/left/right
html,body {height: 100%;overflow: hidden;}
.container {height: 100%;padding: 0 200px;  }
.left,.right{width: 200px;min-height: 200px;background-color: royalblue;}
.left,.center,.right {float: left;}
.center {width: 100%;	min-height: 400px;background: lightsalmon;}
.left{margin-left: -100%;position: relative;	left: -200px;}
.right{margin-right: -200px;}
<div class="container clearfix">
    <div class="center"></div>
    <div class="left"></div>
    <div class="right"></div>
</div>
```

### 2.双飞翼布局

```html
html,body {
    height: 100%;overflow: hidden;
}
.container {width: 100%;}
.left,.container,.right {
	float: left;
}
.container .center {
    margin: 0 200px;
    min-height: 400px;
    background: lightsalmon;
}
.left,.right {
    width: 200px;
    min-height: 200px;
    background-color: royalblue;
}
.left {margin-left: -100%;}
.right {margin-left: -200px;}
<body class="clearfix">
    <div class="container">
        <div class="center"></div>
    </div>
    <div class="left"></div>
    <div class="right"></div>
</body>
```

### 3.flex

```html
html,body {height: 100%;overflow: hidden;}
.container{display: flex;}
.left,.right{
    flex:0 0 200px;
	min-height: 200px;
    background-color: blue;
}
.center{
    flex-grow: 1;	//flex:1;
    min-height: 200px;
    background-color: red;
}
<div class="container">
    <div class="left"></div>
    <div class="center"></div>
    <div class="right"></div>
</div>
```

### 4.定位

```html
html,body {
    height: 100%;
    overflow: hidden;}
.container {
    position: relative;
    height: 100%;
}
.left,.right {
    width: 200px;
    min-height: 200px;
    background-color: royalblue;
}
.center {
    margin: 0 200px;
    min-height: 400px;
    background: lightsalmon;
}
.left {position: absolute;top: 0;left: 0;}
.right {position: absolute;right: 0;top: 0;}
<div class="container">
    <div class="left"></div>
    <div class="center"></div>
    <div class="right"></div>
</div>
```

## 6.移动端响应式方案

```
1.media : PC/移动端一套效果
2.rem ： PC固定布局一套，移动端rem等比缩放一套
3.flex ： 部分的布局结构，不是完整的响应式方案
4.vh、vw ： viewport百分比，类似百分比布局，不是完整的响应式方案
前两种才是完整的主流方案。
```