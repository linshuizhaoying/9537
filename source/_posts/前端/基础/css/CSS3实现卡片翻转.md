---
title: CSS3 实现卡片翻转
toc: true
date: 2017-10-28  18:47:45
tags: [Css, 2017-10]
---

## CSS3 实现卡片翻转
##### 关键属性：
transform-style: flat|preserve-3d;
transition: 有四个过渡属性
* transition-property
* transition-duration
* transition-timing-function
* transition-delay

backface-visibility: visible|hidden
transform: none|transform-functions
##### 实现原理简述
先定一个 box，里面放两个div（card），都是绝对定位，然后让其中一个通过 transform 翻转180度，这样两个 card 就正反面贴在一起了，最后通过给 box 的 hover 效果上，也是用 transform 翻转 180 度，这样就是把背面的翻转到前面来了，前面的翻转到后面，实现一个 card 的翻转。

##### 示例代码
<script async src="//en.jsrun.net/x3iKp/embed/all/light/"></script>
