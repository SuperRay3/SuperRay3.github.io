---
title: MacOS 下安装配置 jdk
date: 2017-08-20 10:12:54
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

## 获取并安装 jdk

[oracle Java Archive 集合下载](https://www.oracle.com/technetwork/java/javase/archive-139210.html)

在上面的链接选择需要的版本进行下载，这里我选择 1.7

![1-1](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/1-1.jpg?x-oss-process=style/blogImg-watermark)

点击 `Accept License Agreemen` 而后点击下载链接进行下载

![1-2](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/1-2.png?x-oss-process=style/blogImg-watermark)

下载完成后，双击打开安装包，一路下一步到底。

打开终端，通过 `java -version` 命令查看是否安装成功

成功后如下图：

![1-3](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/1-3.png?x-oss-process=style/blogImg-watermark)


## 配置环境变量

- 首先定位到 `/etc/profile`

![2-1](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/2-1.png?x-oss-process=style/blogImg-watermark)

- 通过 `sudo vi profile` 对文件进行编辑，
将
```bash
JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.7.0_80.jdk/Contents/Home"
export JAVA_HOME
CLASS_PATH="$JAVA_HOME/lib"
export PATH="$PATH:$JAVA_HOME"
```

![2-2](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/2-2.png?x-oss-process=style/blogImg-watermark)

- 指定 `source` 命令，使修改生效

![2-3](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/2-3.png?x-oss-process=style/blogImg-watermark)

- 检验环境变量是否设置成功 `echo $JAVA_HOME`

![2-4](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/2-4.png?x-oss-process=style/blogImg-watermark)



---

2017-02-26 星期一 23:21

> 不知道是不是因为上述配置原因导致的项目无法启动，错误代码：
<br/>
```
EVERE: Servlet.service() for servlet default threw exception
java.lang.ClassCastException: org.apache.catalina.util.ParameterMap cannot be cast to java.util.HashMap
```
<br/>
错误原因还未能找到，但是因为这个原因接触到了 Mac 下如何卸载 java，方法如下 ⬇️

## 卸载 java

> 参考：[官方卸载方法 java](https://www.java.com/en/download/help/mac_uninstall_java.xml), [官方卸载方法 jdk](https://docs.oracle.com/javase/8/docs/technotes/guides/install/mac_jdk.html)


`卸载 java`

**Note: 需使用管理员权限 sudo**

- 打开终端并输入一下命令分别运行

```bash
sudo rm -fr /Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin
sudo rm -fr /Library/PreferencePanes/JavaControlPanel.prefPane
sudo rm -fr ~/Library/Application\ Support/Java
```

`卸载 jdk`

**Note: 需使用管理员权限 sudo**

- 打开终端并定位到 `/Library/Java/JavaVirtualMachines` ,并且删除下方的 `jdk 文件夹`

![3-1](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/MacOS%20%E4%B8%8B%20jdk%20%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE/3-1.png?x-oss-process=style/blogImg-watermark)






