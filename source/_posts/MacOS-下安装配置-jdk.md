---
title: MacOS 下安装配置 jdk
date: 2018-02-20 10:12:54
tags:
  - java
  - MacOS
categories:
  - 烂笔头
---

> os: macOS High Sierra version 10.13.3 <br/>
  jdk: 1.7.0_80

<!-- more -->

`注： 1.6 版本以下的 jdk oracle 官网没有提供 macOS 版本的下载，如果需要这些版本的需要前往苹果官网进行下载。 ` [点击下载](https://support.apple.com/kb/dl1572?locale=en_GB)

这里主要以 1.7 为例

## 0. 获取并安装 jdk

[oracle Java Archive 集合下载](http://www.oracle.com/technetwork/java/javase/archive-139210.html)

在上面的链接选择需要的版本进行下载，这里我选择 1.7

![1-1](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/1-1.jpg?x-oss-process=style/blogImg-watermark)

点击 `Accept License Agreemen` 而后点击下载链接进行下载

![1-2](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/1-2.png?x-oss-process=style/blogImg-watermark)

下载完成后，双击打开安装包，一路下一步到底。

打开终端，通过 `java -version` 命令查看是否安装成功

成功后如下图：

![1-3](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/1-3.png?x-oss-process=style/blogImg-watermark)


## 1. 配置环境变量

- 首先定位到 `et/profile`

![2-1](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/2-1.png?x-oss-process=style/blogImg-watermark)

- 通过 `sudo vi profile` 对文件进行编辑，
将
```bash
JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.7.0.80_jdk/Contents/Home"

CLASS_PATH="$JAVA_HOME/lib"
```

![2-2](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/2-2.png?x-oss-process=style/blogImg-watermark)

- 指定 `source` 命令，使修改生效

![2-3](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/2-3.png?x-oss-process=style/blogImg-watermark)

- 检验环境变量是否设置成功 `echo $JAVA_HOME`

![2-4](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/2-4.png?x-oss-process=style/blogImg-watermark)

大功告成！

