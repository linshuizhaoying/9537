---
title: css选择器权值
toc: true
date: 2017-10-29  17:53:22
tags: [前端,代码风格标准]
---

  ### CSS选择器权值

  1. 元素,伪元素选择权值 `0,0,0,1`  如: `div`

  2. 类,伪类,属性选择器权值 `0,0,1,0` 如: `.content  :hover  [attribute]`

  3. ID权值 `0,1,0,0`  如: `#main`
  
  4. 内联样式权值 `1,0,0,0`  如: `style="xxx"`

  5. 通配选择符,子选择器,相邻同胞选择器权值为`0`

  ### 匹配法则

  **比较样式的优先级时，只需统计不同选择器的个数，然后与对应的权值相乘即可。根据结果便可得出优先级。**

  * 结果较大的优先级较高

  * 结果相同，则后定义的优先级较高

  * 若样式值中含有 `!important`，则该值优先级最高

    例：

    ```
    #content div#main-content h2 => 100(#content) + 1(div) + 1000(#main-content) + 1(h2) = 202

    #content #main-content>h2 => 100(#content) + 1000(#main-content) + 1(h2) = 201

    body #content div[id="main-content"] h2 => 1(body) + 100(#content) + 1(div) + 10([id="main-content"]) + 1(h2) = 113
    ```

  > [扩展阅读：256个class选择器可以干掉1个id选择器](http://www.zhangxinxu.com/wordpress/2012/08/256-class-selector-beat-id-selector/)

