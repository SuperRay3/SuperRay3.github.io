---
title: Mac 下安装 eclipse Java EE 奇怪问题的解决方法
date: 2018-02-20 17:42:04
tags:
  - java
  - MacOS
categories:
  - 烂笔头
---

> Mac 下在安装 eclipse 时遇到的一个奇怪的问题，然而它的解决方法更加奇怪。

<!-- more -->


## 问题描述

![1-1](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/Mac%20%E4%B8%8B%E5%AE%89%E8%A3%85%20eclipse%20%E5%A5%87%E6%80%AA%E9%97%AE%E9%A2%98%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95/1-1.png?x-oss-process=style/blogImg-watermark)

## 搜寻过程

第一开始以为是先前安装的 jdk 版本不对，因为 相应版本的 eclipse 对应相应的 jdk 版本。如果二者对应不上就会出现打不开的现象。

但是思来想去这个问题觉得原因应该不在于此，于是开始百度。百度错误代码，错误描述什么的都未果，直到无意间找到了知乎的一个问题，看描述和我遇到的基本一致，再看下方的回答表示问题都解决了。于是尝试通过解答是这解决一下自己的问题。具体方法如下，[问题链接](https://www.zhihu.com/question/51409258)

![2-1](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/Mac%20%E4%B8%8B%E5%AE%89%E8%A3%85%20eclipse%20%E5%A5%87%E6%80%AA%E9%97%AE%E9%A2%98%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95/2-1.png?x-oss-process=style/blogImg-watermark)


## 总结

问题的解决方法如同它本身一样令人匪夷所思，只需要将解压出来的 `Eclipse.app` 文件 ***拖***到，记得一定是拖到，不能复制到桌面。然后再拖拽回解压出来的文件夹里，这样问题就解决了......