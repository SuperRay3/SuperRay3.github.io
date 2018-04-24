---
title: 'AngularJS: Service、Factory、Provider'
date: 2018-04-24 08:49:12
tags:
	- javascript
	- AngularJS
categories: 烂笔头 
---

> 最近在接触 `AngularJS`， 被晦涩难懂的各种概念搞得头疼脑涨。`Service`、`Factory`、`Provider` 就是其中几个。

## Factory

Syntax: `module.factory('factoryName', function)`

Result: **the value that is returned by invoking the function reference passed to `module.factory`**

> source code: `return factoryName = fn()`

***Note***
1.  Must return an object which is the main difference differentiates it with other design patterns. We can expose any functionality to where it be injected.

## Services

Syntax: `module.service('serviceName', function)`

Result: **we will be provided with an instance of the function. In other words `new FunctionYouPassedToService()`**

> source code: `return serviceName = new fn()`

***Note:***

1.  Don't need to return any object when create a AngularJS service for it can be instantiated by Angular self.

2.  All we need to do is just add the functionality to `this` variable.


## Provider

Syntax: `module.provider('providerName', function)`

Result: **we will be provided with `(new ProviderFunction()).$get()`**

> source code: `return providerName = (new fn()).$get()`

***Note***

**1.  Provider is one of which can be configured (another is `constant`) during the module configuration phase**

2.  Expose any more functionality through provider add it under `$get` like:
```js
this.$get: function() {
  return {
    name: _name,
    getName: function() {
      return name
    }
  }
}
```

***Additional***

[When an AngularJS app is started, it has a certain "boot-order" (I think it same to life-cycle ?_?). From the perspective of a developer, it looks like this: ](https://tuhrig.de/angularjs-provider-and-app-configuration/)

```js
anuglar.module('myModule', [])
       .config(function(injectables) {  // providers & constants

       })
       .run(function(injectables) {
         // do initialization
       })

```


## reference

[AngularJS: Service vs Factory vs Providers made super simple -- Ng-ninja](http://ngninja.com/posts/angularjs-service-factory-provider)

[AngularJS: Service vs provider vs factory
 -- Stack Overflow](https://stackoverflow.com/questions/15666048/angularjs-service-vs-provider-vs-factory)


## Additional

### Constant

A constant can not be intercepted by a decorator, that means that the value of a constant **should never be changed** (though it is still possible to change it programmatically in Angular 1.x).

### Value

A value is nothing more than a simple injectable value. The value can be a string, number but also a function. **Value differs from constant in that value can not be injected into configurations, but it can be intercepted by decorators.**

### Decorator

A decorator can modify or encapsulate other providers. There is one exception and that a constant cannot be decorated.


##Summary

-  All the providers are instantiated only once. That means that they are all singletons.
All the providers except constant can be decorated.
-  A constant is a value that can be injected everywhere. The value of a constant can never be changed.
-  A value is just a simple injectable value.
-  A service is an injectable constructor.
-  A factory is an injectable function.
-  A decorator can modify or encapsulate other providers except a constant.
-  A provider is a configurable factory.