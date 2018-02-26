---
title: 《Javascript高级程序设计 》 （一） 引用类型
date: 2018-02-14 11:16:49
tags:
  - javascript
categories: 烂笔头
---

> 《Javascript 高级程序设计》 读书系列第一部：引用类型  （文章顺序不是按照书本章节顺序排列）

<!-- more -->

***对象是某个特定引用类型的实例***。新对象是通过使用 `new` 操作符后跟一个**构造函数**来创建的。

构造函数本身就是一个函数，是出于创建新对象的目的而定义的。

`var person = new Object();`

> `new Object()` 已经完成了对象的创建，创建出来的是 `Object` 引用类型的新实例。


## Object 类型

### 创建方式：

  - `new Oject()`

  ```js
    var person = new Object();
    person.name = "ray";
    person.age = 29;

  ```

  - 对象字面量

  ```js
    var person = {
      name: "ray",
      age: 29
    }
  ```

⚠️ 注：上述两种写法在构造函数都是 `Object` 的时候是不会出现问题的，但是以下情况则需要注意：

```js

  // 构造函数
  function Aaa() {

  }

  // 方式一
  Aaa.prototype.name = "ray";
  Aaa.prototype.age = 23;

  // 方式二
  Aaa.prototype = {
    name: "ray",
    age: 23
  }

  var a1 = new Aaa();

  console.log(a1.constructor)
  // 方式一： Aaa()   方式二： Object（）


```

可见利用对象字面量的方式赋值会改写实例的构造函数指向。