---
title: 各终端 Terminal 添加 git 分支名称
date: 2018-04-27 17:39:51
tags:
  - git
categories:
  - 烂笔头
---

> 在终端进行 git 操作的时候，难免会进行分支的切换。切来切去的就会忘记当前所在的分支了。下面我们就在终端中加入 git 的分支信息。

## Mac OS 

在 `~/.bash_profile` 文件中添加以下代码：

```bash
  # Show current git branch name
  parse_git_branch() {
      git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
  }
  export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

## Ubuntu

在 `~/.bashrc` 文件中添加以下代码：

```bash
# Show git branch name
  force_color_prompt=yes
  color_prompt=yes
  parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
  }
  if [ "$color_prompt" = yes ]; then
  PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
  else
  PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w$(parse_git_branch)\$ '
  fi
  unset color_prompt force_color_prompt
```

## reference

[Git branch name in Linux/Mac Terminal](https://gist.github.com/ankurk91/2efe14650d54d7d09528cea3ed432f6d)