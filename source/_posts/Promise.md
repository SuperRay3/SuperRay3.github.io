---
title: Promise
date: 2018-02-17 16:24:50
toc: true
tags:
    - javascript
categories:
    - 烂笔头
---

> 学学 Promise

<!-- more -->


## **0. Timing**

function passed to `.then` will never be called synchronously,even with an already-resolved promise.

```js
Promise.resolve().then(() => console.log(2));
console.log(1) // 1, 2
```

***instead of running immediately, the passed-in function is put on a microtask queue, which means it runs later when the queue is emptied at the end of the current run of the Javascript event loop.***

相对于立即调用，被传入的回调函数会被放置到一个 `microtask` 队列中，这意味着只有当当前的事件循环结束后才会被调用。