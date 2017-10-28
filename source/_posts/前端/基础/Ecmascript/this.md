---
title: this
toc: true
date: 2017-10-28  18:00:56
tags: [前端,js原生,this]
---

### 知识点
- this的指向如何确定
- call, bind, apply
- bind的polyfill写法

### 初级前端的this指向问题
面试过程中考察基础有一道比问题：“this的指向如何确定？”

如何解答这道题目？

我会这样回到：

#### 从作用域说起

作用域分为动态作用域与词法作用域，它们主要的区别是：

1. 词法作用域是在写代码或者说定义的时候确定的，词法作用域关注函数在何处声明
2. 动态作用域是在运行的时候确定的，而动态作用域关注函数从何处调用。

**this就可以类比成js中的动态作用域**

`this`是在运行时进行绑定的，并不是在编写时绑定，它的上下文取决于函数调用的各种条件。`this`的绑定和函数声明的位置没有任何关系，只取决于函数的调用方式。

#### 根据优先级判断this值指向

如果遇到`this`的判断问题，可按照下面的顺序来判断：

##### 函数是否在new中调用（new 绑定）？如果是的话，this 绑定的是新创建的对象。
{% codeblock lang:js %}
function Foo (something) {
  this.a = something
}

let bar = new Foo(3)
console.log(bar.a) // 3
{% endcodeblock %}

##### 函数是否通过call, apply, bind 绑定？如果是的话，this绑定的是指定的对象。

先看 `call`
{% codeblock lang:js %}
function foo () {
  console.log(this.a)
}
const obj = {
  a: 2
}
foo.call(obj) // 2
{% endcodeblock %}

接着看 `bind`
{% codeblock lang:js %}

function foo (sth) {
  return this.a + sth
}
let obj = {
  a: 2
}

let bar = foo.bind(obj)

let b = bar(3)

console.log(b) // 5
{% endcodeblock %}

当说到这里的时候，**可以提一下`call`、`apply`、`bind`的区别**，这里介绍一篇文章[call apply bind 区别](http://www.jianshu.com/p/56a9c2d11adc)
##### 函数是否在某个上下文对象中调用？如果是的话，`this`绑定的就是指定的对象。
{% codeblock lang:js %}
const obj = {
  a: 1,
  foo: function () {
    console.log(this.a)
  }
}
obj.foo() // 1
{% endcodeblock %}

##### 如果都不是的话，使用默认绑定。如果在严格模式下，就绑定到`undefined`，否则绑定到全局对象。

非严格模式：
{% codeblock lang:js %}
var a = 678

function foo () {
  console.log(this.a)
}

var bar = foo() // 678
{% endcodeblock %}

严格模式下：
{% codeblock lang:js %}
'use strict'
var a = ''abc

function foo () {
  console.log(this.a)
}

var bar = foo() // VM3254:2 Uncaught SyntaxError: Unexpected identifier
{% endcodeblock %}

#### 特殊的箭头函数

上面四条可以基本涵盖所有正常的函数，但是，`ES6`中介绍了一种无法使用这些规则的特殊函数类型，箭头函数。

箭头函数是使用 “胖箭头” 的操作符 `=>` 定义的。箭头函数不使用 `this` 的四种标准规则，而是根据外层（函数或者全局）作用域来决定 `this`。

{% codeblock lang:js %}
function foo() {
  return (a) => {
    // this继承自 foo()
    console.log(this.a)
  }
}
var obj1 = {
  a: 2
}

var obj2 = {
  a: 2
}

var bar = foo.call(obj1)
bar.call(obj2) // 2
{% endcodeblock %}

`foo()`内部创建的箭头函数会捕获调用时`foo()`的`this`。由于`foo()`的`this`绑定到`obj1`，`bar`（引用箭头函数）的`this`也会绑定到`obj1`，箭头函数的绑定无法被修改（`new`也不行！）

以上，是初级前端考察 `this` 值指向的一般解答。那么中级前端呢？

### 中级前端的this指向问题
