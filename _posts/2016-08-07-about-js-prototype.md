---
layout: post
title: Javascript的原型链
categories: ComputerScience
---

Javascriptd的原型链是一个比较容易混淆的概念。根据wiki的定义:

	prototype, a property of all JavaScript objects, through which they can inherit further functionality

实际上通过测试却没有得到定义的结果：

```
var obj = {};
console.log(obj.prototype);//undefined
```

如果把这句解释修改为: "all JavaScript function objects"，更为恰当。

```
var func = function(){};
console.log(func.prototype);//{}
```

那么prototype是用来干嘛的呢？根据其字面意思：原型，则应该是作为一个成品背后的基础。成品是根据原型修改来的，成品具备原型应该有的特性，成品可以修改特性，也可以增加特性。

一般，我们获得一个Array对象

```
var arr = [];
```

这是隐式调用了`Array`构造方法。`arr`带有`toString`的方法，这个方法来自`Array.prototype`。这就是`prototype`的威力。需要注意的是，在这个威力发挥的过程中，Array扮演的是构造函数的角色，而它的prototype则是一个对象。这也是为什么容易导致混淆。

`prototype`作为一个对象，他也可以有自己的`prototype`对象。这就产生了原型链（prototype chain）。这个原型链中的每个prototype都需要一个构造函数作为中介。

对象可以通过`__proto__`这个属性来获取自己的prototype对象，并且可以修改。若直接使用`__proto__`，则可以获得更直观的继承效果。

```
var parentparentparent = {
	test:function(){
		console.log("1")
	}
};
var parentparent = {
	// test:function(){
	// 	console.log("2")
	// }
};
parentparent.__proto__ = parentparentparent
var parent = {
	// test:function(){
	// console.log("3")
	// }
};
parent.__proto__ = parentparent;
var child = {};
child.__proto__ = parent;
child.test();
```

不过`__proto__`并不是一个正式的接口，虽然各大浏览器都实现了这个接口。








