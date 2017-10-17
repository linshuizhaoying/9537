---
title: css管理页面布局
toc: true
date: 2017-10-13  11:23:22
tags: [前端,代码风格标准]
---

## 经典三列布局
布局要求：
1、三列布局，中间宽度自适应，两边定宽； 
2、中间栏要在浏览器中优先展示渲染； 
3、允许任意列的高度最高；

## 多栏布局

### 栅格系统(浮动，百分比)

### 多列布局(column-count)

## 弹性布局(flexbox)

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
css3-sizing为width和height定义了新的关键字：min-content将解析为这个容器每部最大的不可断行元素的宽度
