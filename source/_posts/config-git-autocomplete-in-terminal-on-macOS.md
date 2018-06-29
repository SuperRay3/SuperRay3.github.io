---
title: config git autocomplete in terminal on macOS
date: 2018-06-29 15:45:33
tags:
  - git
  - 系统配置
categories: 烂笔头
---

> mac 上的 terminal 竟然不支持 `git` 指令自动补全（应该不是个人原因），这对于使用 `git` 管理代码的程序员或多或少是个麻烦，当然解决方案也很简单。

```
  系统环境：
    macOS Hign Sierra
    version: 10.13.5
```

<!-- more -->

## 下载 bash 文件

```
curl -O https://raw.github.com/git/git/master/contrib/completion/git-completion.bash
```
可能是自己网络的原因，通过上述指令下载下来的文件总是空文件。和我一样的同学可以直接将链接粘贴到浏览器地址栏，然后 `cmd + A & cmd + C` 。

找一个喜欢的文件夹，新建 `.bash` 文件，并将刚才的内容粘贴进文件中。

## source
 - 打开 `terminal`

 - 一路 `cd` 定位到刚才的文件位置

 - 运行 `source <filename>`

 - 重启 `terminal`

 - done!

 ## reference

 [autocompelet git on mac OS](https://stackoverflow.com/questions/4569463/autocomplete-git-in-mac-os-not-working#)
