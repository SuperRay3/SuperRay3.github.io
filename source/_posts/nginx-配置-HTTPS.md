---
title: nginx 配置 HTTPS
date: 2018-02-27 08:56:20
tags:
	- HTTP
	- nginx
categories: 烂笔头
---

> 最近听说谷歌浏览器打算将所有不是通过 `HTTPS` 协议访问的网站标记[(为了全面推行HTTPS，谷歌让自己的Chrome变成了偏执狂)](http://36kr.com/p/5089336.html)为不安全的消息后决定尝试将自己的博客转为 `HTTPS`。这就需要从头到尾的了解一下这究竟是个什么东西，能够实现什么，带来什么好处。下面这篇文章记录了整个过程。

<!-- more -->

```
所用环境配置：

主机：阿里云 CES 1核 1GB
服务器： nginx
操作系统： CentOS Linux release 7.4.1708 (Core)

```

## 什么是 `HTTPS`


