---
title: reflow（重排） 和 repaint（重绘）
date: 2018-03-02 08:45:21
tags:
    - HTML
categories:
    - 烂笔头
---

<!-- more -->

## 是什么

**reflow：** 浏览器重新渲染部分或全部文档，重新计算元素位置和几何解构。页面至少发生一次重排在页面初次加载的时候。

**repaint：** 只改样式而不影响布局，如改： `background-color` 等。

## 触发条件

**reflow**

- **盒模型相关：** `width` `height` `margin` `padding` `border` ...

- **定位、浮动：** `float` `position` ...

- **文字解构：** `text-align` `line-height` `overflow` `font-size` ...

---
- 调整窗口大小

- 样式表变动

- 元素内容变化，尤其是输入控件

- dom操作

- css伪类激活

- 计算元素的offsetWidth、offsetHeight、clientWidth、clientHeight、width、height、scrollTop、scrollHeight

**repaint**

元素更新样式风格相关的属性时。


注 ⚠️：reflow 一定会 repaint，repaint 不一定会 reflow


## 如何避免

**避免 reflow**

本质上是减少对 `render tree` 的操作，`render tree` 包括 `DOM` 和 `CSSOM` 的信息。当二者都组建完毕时才进行 `render tree` 的合并。中途一旦遇到脚本文件就会停止组建，若涉及到对节点或样式的修改会等待修改完毕再继续组建。（这是发生在第一次加载的时候，后续的改变就是描述的那样重排的情况了）

- 直接改类名,减少分别修改样式的次数

```js
// 不好的写法
    var left = 1;
    var top = 2;
    ele.style.left = left + "px";
    ele.style.top = top + "px";
    // 比较好的写法
    ele.className += " className1";
```

或者将几次修改内容拼接成一个字符串，一次性修改，其实原理同上。

```js
    ele.style.cssText += ";
    left: " + left + "px;
    top: " + top + "px;";
```

- 整体搬离，减少 `reflow`

1. 使用[DocumentFragment](https://docs.segmentfault.com/dom/documentfragment)进行缓存操作,引发一次回流和重绘；

 ***DocumentFragment 是 ‘a minimal document object that has no parent.A common use for DocumentFragment is to create one, assemble a DOM subtree within it, then append or insert the fragment into the DOM using Node interface methods such as appendChild() or insertBefore()). ’***

```js
    document.addEventListener('DOMContentLoaded', function () {
        var date = new Date(),
        fragment = document.createDocumentFragment();
    for (var i = 0; i < 7000; i++) {
        var tmpNode = document.createElement("div");
        tmpNode.innerHTML = "test" + i;
        fragment.appendChild(tmpNode);
    }
        document.body.appendChild(fragment);
        console.log("speed time", new Date() - date);
    });
```


2. 使用display:none，只引发两次回流和重绘；

3. 使用cloneNode(true or false) 和 replaceChild 技术，引发一次回流和重绘；

- 频繁访问属性的时候，采取缓存。

```js
// 不好的写法
for(let i = 0; i < 20; i++ ) {
    el.style.left = el.offsetLeft + 5 + "px";
    el.style.top = el.offsetTop + 5 + "px";
}
// 比较好的写法
var left = el.offsetLeft,
top = el.offsetTop,
s = el.style;
for (let i = 0; i < 20; i++ ) {
    left += 5;
    top += 5;
    s.left = left + "px";
    s.top = top + "px";
}
```

- 替代会触发reflow和repaint的属性

比如用translate代替top，用opacity替代visibility

- 减少table的使用

- 动画实现的速度选择

- 对于动画新建图层

## 参考

[reflow和repaint引发的性能问题](https://juejin.im/post/5a9372895188257a6b06132e)

[CSS trigger](https://csstriggers.com/)







