---
title: git 切换分支
date: 2018-02-13 17:15:50
tags: git
categories: 烂笔头
---

> 当从远程仓库克隆出一个项目后， 默认显示项目的default branch（一般为 master）。而我们想要调适其他分支的代码就需要用到 `git` 的切换分支命令了。

<!-- more -->

## **0. 原理**

克隆完成后本地工作区的分支是指向 master 分支的，这时可以通过 `git branch` 命令查看分支情况。

![1-1 ](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%20%E5%88%87%E6%8D%A2%E5%88%86%E6%94%AF/1-1.png?x-oss-process=style/blogImg-watermark)

> `*` 代表当前所在分支

这里的输出结果说明本地代码目前只有一个 master 分支， 使用以下命令查看本地和远程所有的分支

![1-2 ](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%20%E5%88%87%E6%8D%A2%E5%88%86%E6%94%AF/1-2.png?x-oss-process=style/blogImg-watermark)


图上展示的是本地共 1 个分支（master）和远程共 2 个分支（master、src），至于 HEAD 是什么请参考：[HEAD](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840038939c291467cc7c747b1810aab2fb8863508000)


## **1. 操作**

了解项目分支情况，我们就会明白如果想要在本地切换分支，就需要先建立一个与远程分支结构相对应的分支以存储代码。具体操作如下：

![1-3 ](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%20%E5%88%87%E6%8D%A2%E5%88%86%E6%94%AF/1-3.png?x-oss-process=style/blogImg-watermark)

`git checkout -b <新建本地分支名称> <远程主机名称/远程分支名>`

这里的`git checkout -b` 其实是两个命令的缩写形式（表示创建并切换到）。 具体是哪两条：

`git brach src` 和 `git checkout src`

经过以上的操作之后，我们再查看一次所有的分支情况：

![1-4 ](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%20%E5%88%87%E6%8D%A2%E5%88%86%E6%94%AF/1-4.png?x-oss-process=style/blogImg-watermark)

可以看到现在我们的本地和远程仓库的分支情况已经能够对应起来，之后就可以通过 `git checkout <分支名称>` 来自由的切换代码了。


