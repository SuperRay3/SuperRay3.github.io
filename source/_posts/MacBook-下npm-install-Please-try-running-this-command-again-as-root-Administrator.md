---
title: >-
  MacBook 下npm install 'Please try running this command again as
  root/Administrator.'
date: 2018-02-13 19:00:40
tags: git
categories: 烂笔头
---

>刚入手的 Macbook Pro 2017 配置环境遇到的第一个问题就是 `Please try running this command again as
  root/Administrator.` 起初一看第一反应就是权限问题，加 `sudo`。但出于是第一次用 Mac 觉得还是上网搜索一下为好，得到结果后想幸好搜索了一下，问题果然不是那么简单。

<!-- more -->

开篇先吐槽一下百度，搜出来的结果不仅质量差，而且这些低质量的解答还在互相复制，可悲啊。最终决定去外面搜寻答案。

果真已经有过人遇到这个问题，这也是我最终选择的解决方案。

链接如下：
[error installing coffeescript on mac 10.7.2
](https://stackoverflow.com/questions/9027285/error-installing-coffeescript-on-mac-10-7-2/13219572#13219572)

问题的原因确实是权限问题，但是通常用的解决方法也就是直接加 `sudo` 是不推荐的。

![1-1](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%20permission%20denied/1-1.png?x-oss-process=style/blogImg-watermark)

>`$USER` 替换为个人计算机的用户名。

不推荐的原因：

>The npm author recommends not using sudo because packages can run arbitrary commands so sudo npm install is dangerous. He suggests switching the ownership of /usr/local to your user.

参考文章：

  [npm install -g — ERR! Please try running this command again as root/Administrator.](https://ar.al/scribbles/npm-install-g-please-try-running-this-command-again-as-root-administrator/)
