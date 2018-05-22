---
title: Angular Directive
date: 2018-04-27 13:54:54
tags:
	- javascript
	- AngularJS
categories: 烂笔头
---

> 翻译自 [Directives](https://code.angularjs.org/1.5.8/docs/guide/directive)

<!-- more -->

## 隔离指令的作用域(scope)

我们上面的 `myCustomer` 指令已经很棒了，但是它有个致命的缺陷：**只能在给定的作用域里使用它一次。**

上述的缺陷就导致了需要去额外创建多个不同的 `controller` 来达到复用指令的目的。这显然不是好的解决方案。

我们想要做到的是将外部作用域与内部的作用域分离，然后将外部指令映射到内部指令上。这就用到了指令的 `scope` 属性。

<!-- plunker -->

在 `index.html` 中第一个 `<my-customer></my-customer>` 元素将 `info` 属性绑定了 `naomi` 的值，这是我们已经在 `controller` 中暴露出来的。第二个则是绑定到了 `igor`。

**总而言之，在一个 `controller` 中想要复用同一个 `directive` 就需要在 `directive` 中添加 `scope` 属性**
 
 让我们仔细地分析一下 `scope` 这个属性：

 ```js
// ...
scope: {
	customerInfo = '=info'
}
// ...
 ```

 `scope` 属性是一个对象，内容是用于绑定独立作用域。具体如下：

 - `key` 是用于绑定指令的独立作用域的名字
 - `value` 则是告诉 angular 的 `$compile` 在编译的时候将哪个值与视图绑定。

 ***注意：　这些 `＝attr` 属性就像指令名称一样被标准化。将这些属性绑定到元素上时 `<div bind-to-this='thing'>` 需要这样指定　`=bindToThis`***

 如果属性名和和属性值一样，则可以直接使用　`=` 绑定

 ```js
scope: {
	// 等同于　=customer
	customer: '='
}
 ```

 除了使从指令内部绑定不同作用域数据成为可能以外，使用 `isolate scope`　还有另外的影响。

 <!-- plunker -->

 就像名字建议的那样，指令的 `scope` 隔绝了一切除了明确添加到　`scope: {}` 对象中的和 `models`。这对于构建可复用的组件是很有帮助的，因为这阻止了一个组件意外的更改　`model` 中的属性