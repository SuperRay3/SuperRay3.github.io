---
title: CSS 中的 BFC
date: 2017-03-01 08:56:41
tags:
    - CSS
categories:
    - 烂笔头
---

> 外边距怎么不对？ 重叠了，父容器加个 `overflow: hidden;` 就行； 父容器怎么没高度了？ 你子元素是不是设置浮动了？这些工作中经常遇到，通常使用清浮动大法就可解决。但是这背后究竟是什么原理呢？

<!-- more -->

这一切的始作俑者是一个叫 `BFC (Block Formatting Context, 块级格式化上下) ` 的东西在作祟。

## 什么是 `BFC` ？

**`BFC` 是一种 CSS 盒模型的渲染规则**，既然是规则就只需记住无法解释。

## `BFC` 的渲染规则

[Block formatting contexts W3C](https://www.w3.org/TR/CSS21/visuren.html#normal-flow)

- BFC 元素垂直方向上 `margin` 会重叠。 ***正值取最大，正负值相加，负负取绝对值最大***

- BFC元素在页面上是一个独立的容器,外面的元素和里面的元素互不影响。

- BFC元素不会和浮动的元素重叠。(这个可以解释两栏自适应)

- 计算BFC元素的高度时,里面浮动元素的高度也会参与计算 (用来解释overflow:hidden可以清除浮动)




## `BFC` 的触发方式

- 根元素 `html`

- 浮动元素 `float: left / right`

- `overflow` 不为 `visiable`

- `display: inline-block、table-cell、table-caption、table、inline-table、flex、inline-flex、grid、inline-grid`

- `position: absolute、fixed`

注意：display:table也可以生成BFC的原因在于Table会默认生成一个匿名的table-cell，是这个匿名的table-cell生成了BFC。


## 拓展

[三种文档流的定位方案](https://segmentfault.com/a/1190000013023485#articleHeader7)

[前端人人都应该理解的盒模型BFC渲染机制](https://segmentfault.com/a/1190000012988829)








