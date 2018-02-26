---
title: 利用 @font-face 字体图标代替传统图标图片
date: 2017-08-02 08:29:13
tags:
    - CSS
categories:
    - 烂笔头
---

> 项目中经常用到一些细小的图标，常见的方法是让美工做成 `sprite` 图。业务用到的时候通过设置元素背景图，再使用 `background-position` 属性一点点地变化到相应位置达到显示效果。这种方法一旦遇到图标聚集的地方并且还有 `hover` 效果的时候内心可以说是相当崩溃的。

<!-- more -->

# [`@font-face`](http://devdocs.io/css/@font-face) 登台

一言以蔽之，这个 CSS 属性可以让你像操作文本一样操作图标，故而得名字体图标（图标字体）。

这么好用的属性看一看[兼容性](https://caniuse.com/#search=font-face)

![大好河山一片绿啊！](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E5%88%A9%E7%94%A8%20%40font-face%20%E5%AD%97%E4%BD%93%E5%9B%BE%E6%A0%87%E4%BB%A3%E6%9B%BF%E5%9B%BE%E7%89%87%E5%9B%BE%E6%A0%87/0%20-%201%20%E5%85%BC%E5%AE%B9%E6%80%A7.png?x-oss-process=style/blogImg-watermark)

IE6 都能兼容到，虽然是只兼容 `EOT` 格式，但是已经够用，为什么呢？ 因为下面这个平台。

# [IconFont - 阿里巴巴矢量图标库](http://www.iconfont.cn/)

先上几张图，他是长这样的：

![1 - 1 iconfont](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E5%88%A9%E7%94%A8%20%40font-face%20%E5%AD%97%E4%BD%93%E5%9B%BE%E6%A0%87%E4%BB%A3%E6%9B%BF%E5%9B%BE%E7%89%87%E5%9B%BE%E6%A0%87/1%20-%201%20iconfont.png?x-oss-process=style/blogImg-watermark)


![1 - 2 iconfont](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E5%88%A9%E7%94%A8%20%40font-face%20%E5%AD%97%E4%BD%93%E5%9B%BE%E6%A0%87%E4%BB%A3%E6%9B%BF%E5%9B%BE%E7%89%87%E5%9B%BE%E6%A0%87/1%20-2%20iconfont.png?x-oss-process=style/blogImg-watermark)

![1 - 3 iconfont](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E5%88%A9%E7%94%A8%20%40font-face%20%E5%AD%97%E4%BD%93%E5%9B%BE%E6%A0%87%E4%BB%A3%E6%9B%BF%E5%9B%BE%E7%89%87%E5%9B%BE%E6%A0%87/1%20-%203%20iconfont.png?x-oss-process=style/blogImg-watermark)

通过上面的方法，已经能够减少我们很大的工作量了。以前只能使用 `img` 的形式现在完全可以将选中的图标下载为 `svg` 格式的文件然后在浏览器中打开，最后将代码复制到项目中去。

这对于图标不多的地方已经相当实用了，但这还不是这个平台最厉害的地方，最厉害的在下面。

![1 - 5 生成代码](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E5%88%A9%E7%94%A8%20%40font-face%20%E5%AD%97%E4%BD%93%E5%9B%BE%E6%A0%87%E4%BB%A3%E6%9B%BF%E5%9B%BE%E7%89%87%E5%9B%BE%E6%A0%87/1%20-%205%20%E7%94%9F%E6%88%90%E4%BB%A3%E7%A0%81.png?x-oss-process=style/blogImg-watermark)

#### **`@font-face` 的具体使用方法**

[官方文档](http://devdocs.io/css/@font-face)

```css

/* @font-face 属性要单独放在外面 */
@font-face {
	font-family: 'iconfont';
	src: url('//at.alicdn.com/t/font_484185_rucmsm61ix5vobt9.eot');
	src: url('//at.alicdn.com/t/font_484185_rucmsm61ix5vobt9.eot?#iefix') format('embedded-opentype'),
	url('//at.alicdn.com/t/font_484185_rucmsm61ix5vobt9.woff') format('woff'),
	url('//at.alicdn.com/t/font_484185_rucmsm61ix5vobt9.ttf') format('truetype'),
	url('//at.alicdn.com/t/font_484185_rucmsm61ix5vobt9.svg#iconfont') format('svg');
}

/* 使用的时候创建一个类，用 `font-family` 属性去引用 `@font-faily` 属性指定的 `font-family` 值，这样同时针对性的调整 `font-size` 等文本属性了 */
.font-icon {
	font-family: 'iconfont';
}

```

**注意:**
  1. `Web fonts are subject to the same domain restriction (font files must be on the same domain as the page using them), unless HTTP access controls are used to relax this restriction.`

  Web 字体受限于同源策略（字体文件必须和页面在相同的域之下），除非设置了 `CORS` 来放宽限制。

  如果是使用这个平台的代码，我们抓包会看到返回的 `response header` 是下面这个样子的：

  ![1 - 6 使用代码](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E5%88%A9%E7%94%A8%20%40font-face%20%E5%AD%97%E4%BD%93%E5%9B%BE%E6%A0%87%E4%BB%A3%E6%9B%BF%E5%9B%BE%E7%89%87%E5%9B%BE%E6%A0%87/1%20-%206%20%E4%BD%BF%E7%94%A8%E4%BB%A3%E7%A0%81.png?x-oss-process=style/blogImg-watermark)


  # 总结

  `@font-face` 不论从兼容性和方便性来看，都大大超越了传统图片图标的形式，可以放心大胆地在项目中使用了。更多的使用技巧等待着去挖掘。


  ## 相关引用

  [HTTP CORS](http://devdocs.io/http/access_control_cors)

  [阿里巴巴 iconfont](http://www.iconfont.cn/home/index?spm=a313x.7781069.1998910419.2)

  [@font-face](http://devdocs.io/css/@font-face)



