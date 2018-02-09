---
title: new 做了什么？
date: 2018-01-23 15:27:32
tags:
---

这篇博客会先从「创建对象模式」的变化过程讲起，由此能深刻理解构造函数中的`new`到底做了些什么？

---

#### 「`Object`构造函数」

创建自定义对象的最简单方式就是创建一个`Object`的实例，然后再为它添加属性和方法。如下：

	var person = new Object()
	person.name = 'zhao';
	person.walk = function(){
		console.log('走一步的代码')
	} 
##### 转折点：早期的 JS开发人员 经常使用这个模式创建对象。后来，「对象字面量」凭着用更少代码的优势，成为创建对象的首选模式。

---

#### 「对象字面量」

		var person = {
			name: 'zhao',
			walk: function(){
				console.log('走一步的代码')
			}
		}
##### 转折点：「`Object`构造函数」和「对象字面量」都可以创建单个对象，但是这两个方法有个缺点，当使用同一个接口创建多个对象时，会产生大量的重复代码。于是，「工厂模式」应运而生。

---

#### 「工厂模式」
「工厂模式」是指用函数来封装以特定接口创建对象的细节。

	function Foo(name, city){
		this.name = name;
		this.city = city;
		this.walk = function walk(){
	    	console.log('走一步的代码')
		}
		return Foo
	}
	
	var human1 = Foo({name:'zhao', city: 'beijing'})
	var human2 = Foo({name:'zhao', city: 'beijing'})

##### 转折点：「工厂模式」解决了创建同一个接口多个对象的问题，但每次都会返回一个包含多个属性的对象。重点是不能识别一个对象的类型。	

---

#### 「构造函数」
随着`JavaScript`的发展，出现了一种新的模式 ——「构造函数」。

* 构造函数可以创建特定类型的对象。
* 此外，也可以创建自定义的构造函数，从而自定义对象类型的属性和方法。

```
	function Foo(name, city){
		this.name = name;
		this.city = city;
		this.walk = function walk(){
	    	console.log('走一步的代码')
		}
	}
	
	var human1 = new Foo({name:'zhao', city: 'beijing'})
	var human2 = new Foo({name:'zhao', city: 'beijing'})
```
上面代码中，我们看到，与「工厂模式」的不同之处：

1. 没有显式地创建对象
2. 	直接将属性和方法赋给了`this`对象
3. 没有`return`语句
4. 函数名首字母是大写`F`。按照惯例，构造函数始终以大写字母开头，主要是为了区别其他函数。
5. 用了`new`操作符创建新实例。

#### 重点来了，`new`在这里到底干了些什么？
要创建构造函数的新实例，必须使用 `new` 操作符。以这种方式调用构造函数会经历以下步骤：

1.创建一个新对象，这个对象的类型是`object`

```
var human1 = {}
```

2.将构造函数的作用域赋给新对象（因此`this`就指向了这个新对象）

```
human1.__proto__ = Foo.prototype
```

3.执行构造函数中的代码（为这个新对象添加属性）

```
Foo.call(human1)
```

4.返回新对象

---









