---
title: git 实操
date: 2017-08-02 08:29:13
tags:
    - git
categories:
    - 烂笔头
---


> 工作中一直用 svn ，用久了之后感觉还是存在一些说不出来的不方便。以前一直想要接触一下 `git` 但总是因为没有项目可以实践。直到有一天突然想到可以将博文托管到 `github` 上啊，这样不就拥有了项目并且可以实践了吗，于是也就有了下面这篇连载文章，不定期更新~

<!--more-->

#### **[官方文档](https://help.github.com/)是个好东西，一定要利用起来**

# **准备要托管的文件**

可以是项目代码，也可以是文本、图片任何类型文件。我这里就是几篇博文（markdown 格式）

![0-1 项目文件](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%E5%AE%9E%E6%93%8D/0-1%20%E9%A1%B9%E7%9B%AE%E6%96%87%E4%BB%B6.png)

# **初始化一个 `git` 项目**

这里有两种方法：

  - 在 `github` 上直接通过图形化界面引导新建一个 `repository`

  - 通过 `commd line` 的方式在相应的项目文件夹下进行初始化。


### **第一种方式的具体过程如下：**

  - 打开 `github` 上的个人主页, 点击 `New repository` 按钮。按照指导建立新仓库。

  - ![New reporsitoy](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%E5%AE%9E%E6%93%8D/1-%201%20%E5%88%9D%E5%A7%8B%E5%8C%96%20git%20%E9%A1%B9%E7%9B%AE.png)

  - ![确认创建 repository](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%E5%AE%9E%E6%93%8D/1-%202%20%E5%88%9B%E5%BB%BA%20reposito.png)

  - 最够使用 `git clone` 的方式克隆项目到本地

  ![git clone 克隆项目到本地](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%E5%AE%9E%E6%93%8D/1%20-3%20git%20clone.png?x-oss-process=style/blogImg-watermark)


### **下面使用第二种方式：**

  >纯命令行的方式，这种方式的思路其实和第一种是相反的。<br/>
  第一种是通过可视化的方式在远程建立好代码仓库，再克隆到本地的时候就不需要再手动初始化了；<br/>
  第二种方式则是先在本地初始化好 `git` 项目，然后后通过命令行的 `git 指令` 与远程的仓库进行链接，前提也还是要有一个空的仓库。

  以前觉得图形化的方式很方便快捷，但是现在觉得纯命令行的方式使用起来更有成就感。

  具体步骤如下：

  - 进入需要存储项目的目录下，右键呼出 `bash` 命令行窗口。

  ```
    git init 项目名

    e.g.
    git init blog-demo
  ```

  ![git init](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%E5%AE%9E%E6%93%8D/1-4%20git%20init.png?x-oss-process=style/blogImg-watermark)

- 使用 [`git add remote`](https://help.github.com/articles/adding-a-remote/) 与远程仓库链接

现在只是本地创建好了 `git` 项目，还需要和远程的仓库建立起链接才能将代码 `push（推送）` 到远程仓库。

> 注：这里有一个警告，当第一次建立链接后但还没有进行第一次 `pull` 操作前，如果对远程仓库链接进行了 `git remote rename <oldname> <newname>` 的重命名操作`pull` 的操作会出现 `non-fast-forward` 的错误。（暂无解决方案...）



![git remote add 将本地代码与远程仓库建立链接](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%E5%AE%9E%E6%93%8D/1-5%20git%20remote.png?x-oss-process=style/blogImg-watermark)

- 使用 `git remote -v` 查看远程状态

> 通过以上的操作，已经建立起了本地和远程仓库的链接，为下面的文件互相推送构建了基础。

# **`pull` 拉取远程仓库到本地**

`git pull origin master` 上面新建的远程仓库只包含一个 `README.md` 文件，执行过这条指令过后本地仓库就与远程仓库状态同步。

![git pull 拉取远程数据](https://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/git%E5%AE%9E%E6%93%8D/2%20-%201%20git%20pull.png?x-oss-process=style/blogImg-watermark)

相似的操作还有 `git clone, git fetch, git merge` 暂时不详细描述。[相关参考](https://help.github.com/articles/fetching-a-remote/)

# **提交**

`git` 的提交和 `svn` 的提交差别很大，这是由他俩原理决定的。

（未完，后期补）

# **添加 `.gitignore` 文件**

> `.gitignore` 是告诉 `git` 哪些文件是忽略提交的。



[相关阅读](https://help.github.com/articles/ignoring-files/)

```
touch .gitignore  // 创建文件
```

如果要忽略的文件在创建`gitigonre` 文件前已经`checked in`，需要运行一下命令移除。

`$ git rm --cached README.md`

注: 执行完成后，要定位到 `.gitignore` 文件所在路径进行 `push`

## [撤销修改](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374831943254ee90db11b13d4ba9a73b9047f4fb968d000)

这里分为以下两种情况：

- 只是在工作区做了修改，还未 `commit` 到暂存区(stage)中。

- 已经 `commit` 到了暂存区还未 `push` 到远程仓库。

针对情况一：

`git checkout -- <filename>`  退回到最近一次 `git commit` 或 `git add` 状态

`git checkout -- .` 撤销工作区所有文件更改

针对情况二：

`git reset HAED file` 将暂存区的修改撤销掉，重新放回工作区。紧接着可以结合第一种情况的方法继续撤销修改。

## change remote

使用 `https` 方式 clone 下来的代码在每次 `pull` 或者 `push` 时都会要求输入用户名和密码。为了解决这个问题，我们需要将代码的远程仓库地址 `remote` 改为 `SSH`。 具体实现如下：

***https -> SSH***

```git
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

***SSH -> https***

```git
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```
















