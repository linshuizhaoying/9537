---
title: css3打字效果
toc: true
date: 2017-10-13  11:23:22
tags: [前端,代码风格标准]
---
解决方案：
让容器的宽度成为动画的主体，让文本的宽度从0开始以**步进动画**的方式，一个字一个字的扩张到它应有的宽度。
但是这个方法有局限性：不适用于多行文本。
关键属性：setps() -- 逐帧动画
		  ch -- 单位，表示0字形的宽度(在等宽字体中，"0"的宽度和其他字形的宽度一样。)

steps() 是 animation-timing-function 属性的值，这个属性规定了动画的运动曲线，常见的有 linear，ease，ease-in 等。	 
steps(n,[ start | end ] ])，阶梯函数，可以把动画平均分成基本相等的 n 份。但是这个要跟 linear 区分开，linear 之类的过渡函数会在每个关键帧之间插入补间动画，所以动画是连贯性的，而 steps 则是关键帧之间的跳跃。

等宽字体有：Consolas, Monaco, monospace
<p data-height="265" data-theme-id="0" data-slug-hash="KywVqm" data-default-tab="css,result" data-user="xinliqun" data-embed-version="2" data-pen-title="css打字效果" class="codepen">See the Pen <a href="https://codepen.io/xinliqun/pen/KywVqm/">css打字效果</a> by xin (<a href="https://codepen.io/xinliqun">@xinliqun</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>