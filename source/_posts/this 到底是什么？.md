---
title: this 到底是什么？ 
date: 2018-01-19 22:18:01
tags:
---
#### 全局作用域
* 无论是否在严格模式下，在全局执行上下文中（在任何函数体外部）`this`都指代全局对象。
* 在浏览器中，全局对象是`window`。

```
var message = 1
console.log(this.message) // 1
console.log(window.message) // 1
```
---

#### 函数作用域

* 每个函数在被调用时都会自动取得两个特殊变量：`this` 和 `arguments`。除了箭头函数。

* `this`是函数的第一个参数（且必须是对象）,`arguments`是函数的第二个参数（包装成一个数组[]）。

* `this`是参数，所以只有在调用的时候才能确定。

* `this`为什么必须是对象，因为`this`就是函数与对象之间的羁绊。

##### 普通模式：如果`this`是`undefined`或`null`，浏览器会把`this`变成`window`

```
function f(){
	console.log(this)
	console.log(arguments)
}
f.call() // this 是 window
f.call(null) // this 是 window
f.call(undefined) // this 是 window
```

##### 严格模式：默认第一个参数是`undefined`。如果传了第一个参数，那传什么`this`就是什么。

发明`JS`时，被要求要长得像`Java`，让`Java`程序员来学`JS`，但是他们发现`this`多余，就有了 `use strict` 严格模式

```
function f(){
	// 严格模式
  	'use strict';
	console.log(this)
	console.log(arguments)
}
f.call() // this 是 undefined
f.call(null) // this 是 null
f.call(undefined) // this 是 undefined
f.call({name:'frank'}) // {name: 'frank'}, []
f.call({name:'frank'},1,2) // {name: 'frank'}, [1,2]
```
##### 当以对象里的方法的方式调用函数时，它们的`this`是调用该函数的对象

```
var message = {
	name: 'zhao',
	Foo: function (){
		console.log(message)
	}
}
	
message.Foo() // {name: "zhao", Foo: ƒ}
//等同于
this.Foo() // {name: "zhao", Foo: ƒ}
//等同于
this.Foo.call(this) // {name: "zhao", Foo: ƒ}
```


##### 当一个函数用作构造函数时（使用new关键字），它的`this`被绑定到正在构造的新对象。

下面例子中，函数内的`this`被绑定到`human1`对象。

```
function Foo(name, city){
	this.name = 'zhao';
	this.city = 'beijing';
}
	
var human1 = new Foo() 

human1.name // "zhao"
human1.city // "beijing"

```

---

参考：[写代码啦](https://xiedaimala.com/) 
	
