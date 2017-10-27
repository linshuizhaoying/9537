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

这种布局问题在面试中比较常见，适用于pc端，左右两侧有导航或者广告的情况。

#### 脑洞时间

看到这个问题，第一反应是定位，用`position:absolute`将左右两侧内容放在对应的位置。如果你只想看解决方案，请直接跳到**双飞翼布局**！

<p data-height="265" data-theme-id="0" data-slug-hash="KXELzW" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="KXELzW" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/KXELzW/">KXELzW</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
脑洞再大一点，css3有个`calc`计算属性，可以拿来试一下(纯脑洞，不负责兼容😒)。

<p data-height="265" data-theme-id="0" data-slug-hash="aLMrgx" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="aLMrgx" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/aLMrgx/">aLMrgx</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
多列布局其实还可以想到`flex-box`，固定宽度布局，再来试验一下：

虽然这种布局写的css最少，但是需要将left元素提前，就满足不了中间栏优先展示的情况了，anyway，自己权衡。

<p data-height="265" data-theme-id="0" data-slug-hash="vePqNK" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="vePqNK" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/vePqNK/">vePqNK</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

#### 圣杯布局
圣杯布局采用的浮动，相对定位，负边距方法来实现。关键点在于：container要设置padding-left，pading-right，left，right元素通过相对定位使其回到正确的位置。
<p data-height="265" data-theme-id="0" data-slug-hash="YrMPdJ" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="YrMPdJ" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/YrMPdJ/">YrMPdJ</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

#### 双飞翼布局
双飞翼布局和圣杯布局最大的区别就是在center里添加了一个dom节点。
浮动将left,right元素位置回到上一行位置,center占满中间一栏，left，right浮在上面。

<p data-height="265" data-theme-id="0" data-slug-hash="PJXjZB" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="PJXjZB" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/PJXjZB/">PJXjZB</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

### 栅格系统
栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，bootstrap为例 http://v3.bootcss.com/css/#grid-intro

<p data-height="265" data-theme-id="0" data-slug-hash="YrdvQq" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="YrdvQq" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/YrdvQq/">YrdvQq</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script> 

### 多列布局(column-count)
`columns：<column-width> || <column-count>` 这个属性是为了能在web页面中实现类似报纸杂志那种多列排版的布局,这里以三列布局为例。
<p data-height="265" data-theme-id="0" data-slug-hash="QqovwG" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="QqovwG" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/QqovwG/">QqovwG</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## 弹性布局(flexbox)
Flex是Flexible Box的缩写，意为”弹性布局”，用来为盒状模型提供最大的灵活性。
任何一个容器都可以指定为Flex布局。虽然所有浏览器都兼容了这个属性，但是在移动端要用` display:box;display:-webkit-box; `,`display:flex`这个属性不兼容ios4或者一些低端的安卓机。

弹性布局有很多属性，实际开发中我比较常用的情况有2种：
1.三列布局，可以解决用百分比三列布局多出的1%像素。

<p data-height="265" data-theme-id="0" data-slug-hash="BwgybG" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="BwgybG" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/BwgybG/">BwgybG</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
写这个demo的时候，为了明显的看出均分的三部分，给每一部分都加了border，突然想到加了border之后，还是均分的情况，难道flex有类似box-sizing的功能，将边框放在已设定的宽度内绘制？

<p data-height="265" data-theme-id="0" data-slug-hash="YroXLd" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="YroXLd" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/YroXLd/">YroXLd</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
从上面的例子里可以看出，flex属性并没有将border放在已设定的宽度内绘制，而是绘制固定值之后再按比例均分。

2.有固定像素的元素，别的元素自适应。例如：左侧图片固定尺寸，右侧文字宽度占满剩余的宽度。
<p data-height="265" data-theme-id="0" data-slug-hash="vewowR" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="vewowR" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/vewowR/">vewowR</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

下面我们来看下具体的属性
采用Flex布局的元素，称为Flex容器（flex container），简称”容器”。它的所有子元素自动成为容器成员，称为Flex项目（flex item），简称”项目”。

|设置在容器上的属性（6）|设置在项目上的属性（6）|
| ------ | ------ | ------ |
|flex-direction(元素排列方向) | order(排列顺序,默认0)|
|flex-wrap(换行) | flex-grow(定义放大比例,默认0)|
|flex-flow(以上两者的简写) | flex-shrink(定义缩小比例,默认1)|
|justify-content(水平对齐方式) | flex-basis(定义的主轴水平或者垂直,默认auto)|
|align-items(水平对齐方式) | flex(以上三个的缩写，默认0 1 auto)|
|align-content(多行垂直对齐方式) | align-self(单个项目有与其他项目不一样的对齐方式)|



## 流式布局(百分比)

## 瀑布流布局()

## 自适应内部元素(min-content)

前情提要：如果不给一个元素具体的height，它会自适应内容的高度，但是width都是自适应屏幕的宽度，如何让元素自适应内容宽度呢？

下图是自适应屏幕宽度的情况：

<p data-height="265" data-theme-id="0" data-slug-hash="GMwMXQ" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="GMwMXQ" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/GMwMXQ/">GMwMXQ</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
如何让元素自适应内部图片的宽度呢？

<p data-height="265" data-theme-id="0" data-slug-hash="eGQepZ" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="eGQepZ" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/eGQepZ/">eGQepZ</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

css3-sizing为width和height定义了新的关键字：min-content将解析为这个容器每部最大的不可断行元素的宽度。

扩展属性：max-content --表现得好像设置了white-space:nowrap一样
		<p data-height="265" data-theme-id="0" data-slug-hash="QqXoVq" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="max-content" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/QqXoVq/">max-content</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
		  fit-content--可以实现元素收缩效果的同时，保持原本的block水平状态
		  <p data-height="265" data-theme-id="0" data-slug-hash="PJrLyG" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="PJrLyG" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/PJrLyG/">PJrLyG</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

## 垂直居中