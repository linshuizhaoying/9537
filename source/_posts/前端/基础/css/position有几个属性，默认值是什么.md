---
title: position有几个属性，默认值是什么
toc: true
date: 2017-10-29  17:40:21
tags: [Css,2017-10]
---

## position有几个属性，默认值是什么
##### 属性：
{% codeblock lang:js %}
position: static|relative|absolute|fixed|inherit
{% endcodeblock %}

* static:
默认值，没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）
* relative:
生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的左侧位置添加 20 像素的偏移
* absolute:
生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
* fixed:
生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
* inherit
规定应该从父元素继承 position 属性的值

##### css3动画keyframe可以使用哪些属性
除了static, 其他的都可以使用

##### 示例代码
<script async src="//en.jsrun.net/j3iKp/embed/all/light/"></script>
