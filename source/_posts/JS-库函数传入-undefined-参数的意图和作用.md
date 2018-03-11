---
title: JS 库函数传入 undefined 参数的意图和作用
date: 2017-04-13 13:29:30
summary: 记一次由箭头函数引发的一连串思考
tags:
	- javascript
	- ES6
categories: 烂笔头
---
> &emsp;&emsp;最近了解 ES6 的箭头函数时无意间扯出了一连串的问题。首先碰到了 bind() 函数，先前只了解call() 和 apply() 不曾注意到 bind(),于是视线暂时转移到 bind()。
&emsp;&emsp;当搜索 MDN 时发现 bind() 根据参数个数的不同分为不同的功能，其中手册中的例子在演示传入两个参数时第一个参数传入 undefined 这让我想起来了在 jQuery 框架中也曾经见到这样的做法但一直懒惰不去仔细了解，于是这个问题链的终点就停在此，我将以“递归”的方式从前往后发现问题，从后往前解决问题。

<!--more-->

### jQuery 为什么将 undefined 当作参数传入？

> &emsp;&emsp;防止 window.undefined 被重写，由于 undefined 不是 JS 的保留字，所以存在开发者在全局作用域声明一个名为 undefined 的变量并赋值的情况。当开发者自己编写的函数内部用到了 window.undefined 在寻找时追溯到顶层作用域而此时发现已被重写，就会导致意外发生。值得注意的是这个问题只存在于一些老的浏览器，当时的规则 undefined 是可以被重写的。而当 ES 5 出台后规定全局作用域中的 window.undefined 是不能被写的，而函数作用域的依旧可以。

jQuery 为了兼容旧浏览器的做法

```js
	(function(window,undefined){
		// xxx
	})(window)
```

这种解决方案的关键点在于`设定 undefined 形参，但不传入对应的实参。这样可以保证将 window.undefined 传入函数内部。`。
这里有个知识点：**JS 中缺省的参数，默认传递 undefined**。
当函数内部需要用到 undefined 时会先在内部作用域查找，而此时 undefined 已被传递进来并且是被赋为 window.undefined ，所以就停止了向上查找，排除了 window.undefined 被重写造成的影响。
`这种情况只存在于老旧浏览器, window.undefined 可被重写的 bug 。随着时间的发展，这种写法已不再使用，因为没有必要再兼容老旧浏览器`

### bind() 函数：两套参数，两种功能

> &emsp;&emsp;bind()方法会**创建一个新函数**。当这个新函数被调用时，bind()的*第一个参数将作为它运行时的 **this**, 之后的一序列参数将会在传递的实参前传入作为它的参数。 引自 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

#### 一个参数：创建一个函数，使这个函数不论怎么调用都有同样的 this 值。

```JS
	this.x = 9;
	var module = {
		x: 81,
		getX: function() {
			return this.x
		}
	}

	module.getX()
	var retrieveX = module.getX  // retrieveX 拿到 getX 指针
	retrieveX()  // 等价于 window.retrieveX 结果为 9

	// bind() 登场

	var boundGetX = retrieveX.bind(module)   // 此处的 module 就是永久绑定到的 this, 注意他会返回一个新的函数
	boundGetX()  //81


```

#### 两个参数：使一个函数拥有预设的初始参数

```JS
function list() {
  return Array.prototype.slice.call(arguments);
}

var list1 = list(1, 2, 3); // [1, 2, 3]

// Create a function with a preset leading argument
var leadingThirtysevenList = list.bind(undefined, 37);

var list2 = leadingThirtysevenList(); // [37]
var list3 = leadingThirtysevenList(1, 2, 3); // [37, 1, 2, 3]

```
[bind() 的详细讲解](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

#### 手写 `bind()`

```js
	function bind(fn, context){
		return function (){
			return fn.apply(context, arguments);
		}
	}
```

上述代码包含两个知识点：
1. Array.prototype.slice.call(arguments) 可以将一个具有 length 属性的对象转化为数组
2. 当需要传的实参数量少于形参的数量时，可以用 undefined 占位。
