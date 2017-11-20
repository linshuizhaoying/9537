---
title: css选择器权值
toc: true
date: 2017-10-29  17:53:22
tags: [前端,代码风格标准]
---

  ### CSS选择器权值

  1. 元素,伪元素选择权值 `1`  如: `div`

  2. 类,伪类,属性选择器权值 `10` 如: `.content  :hover  [attribute]`

  3. ID权值 `100`  如: `#main`
  
  4. 内联样式权值 `1000`  如: `style="xxx"`

  5. 通配选择符,子选择器,相邻同胞选择器权值为`0`

  ### 匹配法则

  **比较样式的优先级时，只需统计不同选择器的个数，然后与对应的权值相乘即可。根据结果便可得出优先级。**

  * 结果较大的优先级较高

  * 结果相同，则后定义的优先级较高

  * 若样式值中含有 `!important`，则该值优先级最高

    例：

    ```
    #content div#main-content h2的权值计算结果:
    100 + 1 + 1000 + 1 = 202

    #content #main-content>h2的权值计算结果:
    100+ 100 + 1 = 201

    body #content div[id="main-content"] h2的权值计算结果:
    1 + 100 + 1 + 10 + 1 = 113
    ```

  > [扩展阅读：256个class选择器可以干掉1个id选择器](http://www.zhangxinxu.com/wordpress/2012/08/256-class-selector-beat-id-selector/)

