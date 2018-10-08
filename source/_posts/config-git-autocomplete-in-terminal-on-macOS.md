---
title: Mac 环境下为通过 homebrew 安装的 git 添加指令自动补全功能
date: 2018-06-29 15:45:33
tags:
  - git
categories: 烂笔头
---

> 本方法目前只针对通过 `homebrew` 安装的 `git`。

<!-- more -->

# 使用 `homebrew` 安装 `git bash-completion`

如果机子还未安装 `homebrew`，打开终端并输入下面这条命令：

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

如果机子已经安装 `homebrew`， 则直接运行下面这条指令：

```bash
brew install git bash-completion
```

# 修改 `~/.bash_profile`

在 `~/.bash_profile` 中添加下方代码：

```
if [ -f $(brew --prefix)/etc/bash_completion ]; then
    . $(brew --prefix)/etc/bash_completion
fi
```


# 参考

[Homebrew’s `git` not using completion -- stackoverflow](https://stackoverflow.com/questions/14970728/homebrew-s-git-not-using-completion)










