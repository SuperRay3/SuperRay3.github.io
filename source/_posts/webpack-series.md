---
title: webpack series
date: 2018-04-24 21:46:57
tags:
  - webpack
categories:
  - 烂笔头
---

> 买了本掘金小册 《使用 webpack 定制前端开发环境》，决定跟着学一遍 webpack。在此不定期打卡记录一下。

<!-- more -->

## webpack 的概念和基础使用

### loader

webpack 使用 loader 将不同格式的文件转换为 webpack 所支持的 **模块**。

支撑着 webpack 处理文件的多样性。

### plugin

用于处理 loader 功能以外的其他任务，例如： 压缩 JS

## webpack 如何解析代码模块路径

常用的几个如下方代码里所注释的：

```js
module.exports = {

  ...

  resolve: {
    // import 时的代号，顾名思义是针对于 js 文件的模块引用
    alias: {
      utils: path.resolve(__dirname, 'src/utils'),
      log$: path.resolve(__dirname, 'src/utils/log.js')
    },
    // 用于 import 模块时自动匹配后缀名称
    extensions: ['.js', '.json', '.jsx', '.css', '.less'],
    // modules 顾名思义为 node 的模块，所以默认就为当前文件下的 node_modules 文件夹。
    // 此处写绝对路径的原因是为了导出的时候更加方便查找减少时间
    modules: [
      path.resolve(__dirname, 'node_modules')
    ]
  }

  ...
}

```

