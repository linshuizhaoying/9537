---
title: css管理页面布局
toc: true
date: 2017-10-13  11:23:22
tags: [前端,代码风格标准]
---

## 多栏布局

### 经典三列布局(浮动，负边距)

布局要求：

1、三列布局，中间宽度自适应，两边定宽； 

2、中间栏要在浏览器中优先展示渲染； 

3、允许任意列的高度最高；

这种布局问题在面试中比较常见，适用于 pc 端，左右两侧有导航或者广告的情况。

#### 脑洞时间

看到这个问题，第一反应是定位，用 `position:absolute` 将左右两侧内容放在对应的位置。如果你只想看解决方案，请直接跳到**双飞翼布局**！

<p data-height="265" data-theme-id="0" data-slug-hash="KXELzW" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="KXELzW" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/KXELzW/">KXELzW</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

脑洞再大一点，css3 有个 `calc` 计算属性，可以拿来试一下(纯脑洞，不负责兼容😒)。

<p data-height="265" data-theme-id="0" data-slug-hash="aLMrgx" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="aLMrgx" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/aLMrgx/">aLMrgx</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

多列布局其实还可以想到 `flex-box`，固定宽度布局，再来试验一下：

虽然这种布局写的 css 最少，但是需要将 left 元素提前，就满足不了中间栏优先展示的情况了,anyway,自己权衡。

<p data-height="265" data-theme-id="0" data-slug-hash="vePqNK" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="vePqNK" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/vePqNK/">vePqNK</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

#### 圣杯布局
圣杯布局采用的浮动，相对定位，负边距方法来实现。关键点在于：container 要设置 padding-left，pading-right，left，right 元素通过相对定位使其回到正确的位置。

<p data-height="265" data-theme-id="0" data-slug-hash="YrMPdJ" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="YrMPdJ" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/YrMPdJ/">YrMPdJ</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

#### 双飞翼布局
双飞翼布局和圣杯布局最大的区别就是在center里添加了一个 dom 节点。
浮动将 left,right 元素位置回到上一行位置,center占满中间一栏，left，right 浮在上面。

<p data-height="265" data-theme-id="0" data-slug-hash="PJXjZB" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="PJXjZB" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/PJXjZB/">PJXjZB</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

### 栅格系统
栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，bootstrap 为例 http://v3.bootcss.com/css/#grid-intro

<p data-height="265" data-theme-id="0" data-slug-hash="YrdvQq" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="YrdvQq" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/YrdvQq/">YrdvQq</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script> 

### 多列布局( column-count )
`columns：<column-width> || <column-count>` 这个属性是为了能在 web  页面中实现类似报纸杂志那种多列排版的布局,这里以三列布局为例。

<p data-height="265" data-theme-id="0" data-slug-hash="QqovwG" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="QqovwG" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/QqovwG/">QqovwG</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## 弹性布局( flexbox )
Flex 是 Flexible Box 的缩写，意为“弹性布局”，用来为盒状模型提供最大的灵活性。
任何一个容器都可以指定为 Flex 布局。虽然所有浏览器都兼容了这个属性，但是在移动端要用 ` display:box;display:-webkit-box; `,`display:flex`  这个属性不兼容 ios4 或者一些低端的安卓机。

弹性布局有很多属性，实际开发中我比较常用的情况有2种：
1.三列布局，可以解决用百分比三列布局多出的 1% 像素。

<p data-height="265" data-theme-id="0" data-slug-hash="BwgybG" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="BwgybG" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/BwgybG/">BwgybG</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

写这个 demo 的时候，为了明显的看出均分的三部分，给每一部分都加了 border，突然想到加了 border 之后，还是均分的情况，难道 flex 有类似 box-sizing 的功能，将边框放在已设定的宽度内绘制？

<p data-height="265" data-theme-id="0" data-slug-hash="YroXLd" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="YroXLd" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/YroXLd/">YroXLd</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

从上面的例子里可以看出，flex 属性并没有将border放在已设定的宽度内绘制，而是绘制固定值之后再按比例均分。
2.有固定像素的元素，别的元素自适应。例如：左侧图片固定尺寸，右侧文字宽度占满剩余的宽度。

<p data-height="265" data-theme-id="0" data-slug-hash="vewowR" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="vewowR" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/vewowR/">vewowR</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

下面我们来看下具体的属性
采用Flex布局的元素，称为 Flex 容器（ flex container ），简称”容器”。它的所有子元素自动成为容器成员，称为 Flex 项目（ flex item ），简称”项目”。

|设置在容器上的属性（6）|设置在项目上的属性（6）|
| ------ | ------ | ------ |
|flex-direction(元素排列方向) | order(排列顺序,默认0)|
|flex-wrap(换行) | flex-grow(定义放大比例,默认0)|
|flex-flow(以上两者的简写) | flex-shrink(定义缩小比例,默认1)|
|justify-content(水平对齐方式) | flex-basis(定义的主轴水平或者垂直,默认auto)|
|align-items(水平对齐方式) | flex(以上三个的缩写，默认0 1 auto)|
|align-content(多行垂直对齐方式) | align-self(单个项目有与其他项目不一样的对齐方式)|

再具体讲属性之前，我们先来了解下 flex 容器默认存在的两根轴，借用下阮老师的图
<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png" alt="">

水平的主轴（ main axis ）和垂直的交叉轴（ cross axis ）。主轴的开始位置（与边框的交叉点）叫做 main start，结束位置叫做 main end；交叉轴的开始位置叫做 cross start，结束位置叫做 cross end。
项目默认沿主轴排列。单个项目占据的主轴空间叫做 main size，占据的交叉轴空间叫做 cross size。

##### 设置在容器上的属性1: flex-direction (元素排列方向)

flex-direction：
	row（默认值）：主轴为水平方向，起点在左端。
	row-reverse：主轴为水平方向，起点在右端。
	column：主轴为垂直方向，起点在上沿。
	column-reverse：主轴为垂直方向，起点在下沿。

<p data-height="265" data-theme-id="0" data-slug-hash="GOrRbR" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="flex-direction" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/GOrRbR/">flex-direction</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

从代码结构中可以看出，flex 可以将块级子元素变成像行内块级元素一样排列。如果你有一个三天两头换布局左右排序的 ui，强烈推荐你使用这个属性。可以通过改变属性 row-reverse 达到右浮动的效果，但是又不需要去管浮动导致的脱离标准流的后果。

<p data-height="265" data-theme-id="0" data-slug-hash="rYYJmj" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="rYYJmj" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/rYYJmj/">rYYJmj</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

##### 设置在容器上的属性2: flex-wrap (换行)

flex-wrap：
	nowrap (默认值)：不换行
	wrap：换行，第一行在上方
	wrap-reverse：换行，第一行在下方

<p data-height="265" data-theme-id="0" data-slug-hash="KyyQoz" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="KyyQoz" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/KyyQoz/">KyyQoz</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

从上面的例子里可以看出，nowrap 属性可以忽略子元素的 width 属性，使其按照比例均分整个父元素的宽度。

<p data-height="265" data-theme-id="0" data-slug-hash="jaQQPy" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="jaQQPy" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/jaQQPy/">jaQQPy</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

从上面的例子可以看出，wrap 和 wrap-reverse 都不会改变子元素的 width，并且会换行，不过 wrap-reverse 会把第一行放在最下面，倒着往上排。

##### 设置在容器上的属性3: flex-flow 

flex-flow 是 flex-direction 和 flex-wrap 的合写，默认值 row nowrap。
flex-flow: flex-direction || flex-wrap

##### 设置在容器上的属性4: justify-content 

## 流式布局(百分比)

## 瀑布流布局()

## 自适应内部元素( min-content )

前情提要：如果不给一个元素具体的 height ，它会自适应内容的高度，但是 width 都是自适应屏幕的宽度，如何让元素自适应内容宽度呢？

下图是自适应屏幕宽度的情况：

<p data-height="265" data-theme-id="0" data-slug-hash="GMwMXQ" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="GMwMXQ" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/GMwMXQ/">GMwMXQ</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

如何让元素自适应内部图片的宽度呢？

<p data-height="265" data-theme-id="0" data-slug-hash="eGQepZ" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="eGQepZ" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/eGQepZ/">eGQepZ</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

css3-sizing 为 width 和 height 定义了新的关键字：min-content 将解析为这个容器每部最大的不可断行元素的宽度。

扩展属性：max-content --表现得好像设置了 white-space:nowrap 一样

<p data-height="265" data-theme-id="0" data-slug-hash="QqXoVq" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="max-content" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/QqXoVq/">max-content</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

fit-content--可以实现元素收缩效果的同时，保持原本的block水平状态

<p data-height="265" data-theme-id="0" data-slug-hash="PJrLyG" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="PJrLyG" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/PJrLyG/">PJrLyG</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## 垂直居中