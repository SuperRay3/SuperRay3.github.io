---
title: JS 的非数字下标数组
date: 2017-07-11 14:11:00
toc: true
tags:
    - javascript
categories:
    - 烂笔头
---
>Javascript 的数组虽然能够通过非数字下标获取数组元素，但是本质上它和 PHP 等语言的关联数组（数组下表不是数字而是字符串）并不一样。详细原理和特殊表现**详见下文**。

<!--more-->

### “正常人思路”
~~~js
    var array = [] ;
    array["a"] = "hello";
    array["b"] = "world" ;
    console.log("length:"+array.length);
~~~
正常思路认为结果输出应该为 `length:2`。

### “非正常输出”
但灵活的 Javascript 在上述问题有着别样的处理方法，实际的输出结果为 `length:0`。这是为什么？

我们将代码稍作改动,再看结果。
~~~js
    var array = [] ;
    array["a"] = "hello";
    array["b"] = "world" ;
    array["10"] = "!";
    console.log("length:"+array.length);
~~~

![目瞪口呆.jpg](http://myblog-static.oss-cn-beijing.aliyuncs.com/post-imgs/js-%E7%9A%84%E9%9D%9E%E6%95%B0%E5%AD%97%E4%B8%8B%E6%A0%87/img1.png?x-oss-process=style/blogImg-watermark)

### 事情的真相
Javascript 数组的下标存在一个范围值（0~2^32）。对于给定的下标值不在此范围内，JavaScript 就会将下标值转化为字符串，并将该字符串对应的值作为数组的该数组`对象的属性值`而不是数组的元素。例如`array[-1]`就是给`array`对象添加了一个名为“-1”的属性值。

如果下标值在有效范围，不论值得类型是数字还是字符串，JavaScript 都会强制转化为数字。`array[100]`如果前方之前没有值，JavaScript 会自动填充，并且数组的`length`为100。

