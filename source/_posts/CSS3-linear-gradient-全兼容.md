---
title: CSS3 linear-gradient 全兼容
date: 2018-02-28 11:03:02
tags:
    - CSS
categories:
    - 烂笔头
---

> 一次项目中遇到了 IE10 以上浏览器渐变失效的问题。以前在 CSS3 属性上遇到兼容问题就从网上找一段代码方式也不测试（懒）就过，这次测试人员测出来了问题，于是决定梳理一下。

<!-- more -->

## 兼容性

![1-1]()

通过检测发现 `linear-gradient` 在 IE 上只有 10 以上支持，那我们在书写的过程中就要考虑到 8 以下该如何兼容。

## synax

```css
 /* 旧语法 */
 background: -prefix-linear-gradient(top, blue, white)


 /* 新语法 */
 background: -prefix-linear-gradient(to bottom, blue, white)
```

***详细用法参考 [深入理解CSS3 gradient斜向线性渐变](http://www.zhangxinxu.com/wordpress/2013/09/%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3css3-gradient%E6%96%9C%E5%90%91%E7%BA%BF%E6%80%A7%E6%B8%90%E5%8F%98/)***

IE 10 以上完美支持新语法，其他浏览器同样支持。

新语法与旧语法的区别在于，新语法不需要再去写浏览器前缀，并且在第一个参数前加上了 `to` 来表示渐变结束方向，不同于旧语法的直接写开始方向。

> 新语法去前缀加 `to`

## 兼容 IE 6~8

由于这些浏览器较古老无法支持新特性。但是在当时的环境下 IE 还是有自己的独门武器就是滤镜，这在当时超于同行的。

可以通过 IE 的上述滤镜功能来实现渐变效果，具体方法如下：

```css
filter: progid:DXImageTransform.Microsoft.Gradient(startcolorstr, endcolorstr, gradientType)
```

参数说明：

`startcolorstr`: 渐变起始颜色

`endcolorstr`: 渐变结束颜色

`gradientType`: [0 | 1] 0 代表纵向渐变，1 代表横向渐变

> IE9 以下同样不支持 `opacity` 和 `rgba()`,所以也就无法实现透明渐变，这个问题同样需要滤镜来实现了。

```css
filter:alpha(opacity=100 finishopacity=0 style=1 startx=0,starty=5,finishx=90,finishy=60)
```

其中各个参数的含义如下：

opacity表示透明度，默认的范围是从0 到 100，他们其实是百分比的形式。也就是说，0代表完全透明，100代表完全不透明。

finishopacity 是一个可选参数，如果想要设置渐变的透明效果，就可以使用他们来指定结束时的透明度。范围也是0 到 100。

style用来指定透明区域的形状特征：
0 代表统一形状

1 代表线形

2 代表放射状

3 代表矩形。

startx 渐变透明效果开始处的 X坐标。

starty 渐变透明效果开始处的 Y坐标。

finishx 渐变透明效果结束处的 X坐标。

finishy 渐变透明效果结束处的 Y坐标。

## 参考

[MDN 使用CSS渐变](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Using_CSS_gradients)

[CSS实现兼容性的渐变背景(gradient)效果](http://www.zhangxinxu.com/wordpress/2010/04/css%E5%AE%9E%E7%8E%B0%E5%85%BC%E5%AE%B9%E6%80%A7%E7%9A%84%E6%B8%90%E5%8F%98%E8%83%8C%E6%99%AFgradient%E6%95%88%E6%9E%9C/)









