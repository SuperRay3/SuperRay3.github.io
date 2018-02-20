---
title: 解决 Enter passphrase key 问题
date: 2018-02-20 22:46:48
tags:
  - ssh
categories:
  - 烂笔头
---

> 在本地生成 `id_rsa` 的时候对其设定了 `passphrase` ,以至于后来每次向 `github` 仓库 `push` 的时候都要手动输入一次 `passphrase` 才验证身份，这样虽然保证了安全性，但是大大降低了便捷性。所以就去搜寻了解决方案。

<!-- more -->

## 0. 解决方法

本地依次运行以下代码：

```bash
eval `ssh-agent`
ssh-add
```

![1-1](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E8%A7%A3%E5%86%B3-Enter-passphrase-key-%E9%97%AE%E9%A2%98/1-1.png?x-oss-process=style/blogImg-watermark)

![1-2](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E8%A7%A3%E5%86%B3-Enter-passphrase-key-%E9%97%AE%E9%A2%98/1-2.png?x-oss-process=style/blogImg-watermark)

`ssh-agent` 是用于管理密钥，`ssh-add` 用于将密钥加入到 `ssh-agent` 中，`SSH` 可以和 `ssh-agent` 通信获取密钥，这样就不需要用户手工输入密码了。

将以上命令写入到 `~/.bash_profile` 中，可以免去每次重启会话都要重新输入上述两条命令的麻烦。

![1-3](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E8%A7%A3%E5%86%B3-Enter-passphrase-key-%E9%97%AE%E9%A2%98/1-3.png?x-oss-process=style/blogImg-watermark)

***如上的命令只对当前会话有效，当会话关闭立马就会失效。***

## 1. 永久性解决问题

**利用 `Keychain`**

> **Add Identity Using Keychain**<br/> to persist the passphrase through restarts by storing it in your keychain, you can use the -K option when adding the identity like this:`ssh-add -K ~/.ssh/id_rsa`<br/>
Once again, this will ask you for the passphrase, enter it and this time it will never ask again for this identity.

![2-1](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/%E8%A7%A3%E5%86%B3-Enter-passphrase-key-%E9%97%AE%E9%A2%98/2-1.png?x-oss-process=style/blogImg-watermark)

第一点中提到的解决方法就是没有利用 `keychain` 来管理密码。持久性只能保持到当前会话。






