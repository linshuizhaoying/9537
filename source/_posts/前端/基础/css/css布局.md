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

看到这个问题，第一反应是定位，用`position:absolute`将左右两侧内容放在对应的位置。

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

### 多列布局

<p data-height="265" data-theme-id="0" data-slug-hash="QqovwG" data-default-tab="html,result" data-user="xinliqun" data-embed-version="2" data-pen-title="QqovwG" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/QqovwG/">QqovwG</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
## 弹性布局(flexbox)
弹性布局模型中，容器会根据布局的需要，调整其中包含的条目的尺寸和顺序来最好地填充所有可用的空间。
容器的尺寸发生变化时，其中包含的条目也会被动态地调整。
弹性盒布局内在的方向限制，可以由开发人员自由操作。

弹性布局有很多属性，我比较常用的情况有2种：
1.3列布局，可以解决用百分比3列布局多的那点像素。
2.有固定像素的元素，别的元素自适应。






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

		  fit-content--可以实现元素收缩效果的同时，保持原本的block水平状态

## 垂直居中