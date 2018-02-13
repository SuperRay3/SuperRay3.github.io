---
title: git clone 时遇到 Permission denied (publickey) 怎么办？
date: 2017-11-05 00:41:35
tags:
  - git
categories:
  - 烂笔头
---
> 如果在 `git clone` 时遇到 `Permission denied (publickey)` 怎么解决？

<!--more-->

这个问题的原因可能有多个，以下解决方法不能保证都能见效。先记录下来，回头研究透彻再补充。

### 问题带来的影响

不能 clone repository。

### 解决步骤

- 0. First you'll want to cd into your .ssh directory. Open up the terminal and run:
```bash
cd ~/.ssh && ssh-keygen
```

- 1. 复制 SSH Key 到剪贴板
OS X: `cat id_rsa.pub | pbcopy`
Linux: `cat id_rsa.pub | xclip`
Windows: `cat id_rsa.pub | clip`

- 2. 打开 github 个人主页， 点击头像， 选择 setting -> SSH and GPG keys

![SSH and GPG keys 设置](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/github%20%E9%85%8D%E7%BD%AE%20SSH%20Key/New%20SSH%20key.png?x-oss-process=style/blogImg-watermark)

点击 `New SSH key`

![New SSH key](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/github%20%E9%85%8D%E7%BD%AE%20SSH%20Key/SSH%20and%20GPG%20keys.png?x-oss-process=style/blogImg-watermark)

在 key 文本域中 `Ctrl + v`， title 文本域随便起一个自己能分辨的名称即可。

- 3. Done!

----

**补充理解 2018-01-29 09:12 星期一**

经过一些实践发现上述过程其实只是在本地生成 `SSH密钥` 并通过 github 网站提供的方法将本地密钥与 github 账户进行关联，这样用户自己就可以在 github 上创建仓库并通过 `use SSH` 的方式 clone 仓库代码到本地了。

上述的过程并不是问题的解决方式。因为上述问题出现在自己克隆别人仓库的项目时出现的。在这个克隆过程中选择了通过 `use SSH` 的方式导致了错误的出现。错误原因是仓库作者并没有将用户的 `SSH 密钥` 添加到自己的信任列表中，所以就不能 clone 项目代码。

解决方法： `use HTTP`

### 参考

[Git - Permission denied (publickey)](https://stackoverflow.com/questions/2643502/git-permission-denied-publickey)

