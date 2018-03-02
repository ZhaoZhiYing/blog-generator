---
title: JS 立即执行函数和闭包
date: 2018-02-19 12:54:59
categories: JavaScript
tags:
---

#### 执行环境和作用域

##### 执行环境
* 「执行环境」定义了变量或函数有权访问的其他数据，决定了它们各自的行为。
* 每个「执行环境」都有一个与之关联的「变量对象」，环境中定义的所有变量和函数都保存在这个对象中。

##### 作用域
* 当代码在一个「执行环境」中时，会创建「变量对象」的一个「作用域链」。
* 「作用域链」的用途是保证对`执行环境`有权访问的所有变量和函数的有序访问。

* 「作用域」分为**全局作用域**和**局部作用域(也叫函数作用域)**
「全局变量」，「函数作用域」中声明的变量是「局部变量」。
* 外部无法读取「局部变量」，但函数内部可以读取「全局变量」。同名的「局部变量」会在函数内部覆盖「全局变量」。  

```
var name = 'zhao'
function foo(){
	var name = 'tang'
	console.log(name)
}
foo()//tang

//函数 foo 内部的变量 name 覆盖了全局变量 name
```


##### 堆栈`Call Stack`先入后出
* 每个函数都有自己的「执行环境」。「执行环境」是用环境栈来管理的。
* 最底层的是「全局执行环境」（在浏览器中，指`Window对象`），当执行到一个函数，函数的「执行环境」就会被推入到「环境栈」中。如果在函数中继续执行函数，那么内部函数的「执行环境」就继续被推入「环境栈」。

```
function a(){
	console.log('a')
	return a
}
a.call() 
	
* 当调用时，a.call() 会被记在 call stack 里。
* 接着 console.log('a') 记在 call stack 里。
* return a 到这一步时 console.log('a') 会存在 a.call() 里，最后 a.call() 退出。
```

---

#### 「立即执行函数」

* 全局变量会造成同名覆盖的问题。
* 解决办法：声明局部变量。
* `ES6` 之前，只有函数才有局部变量。
* `立即执行函数`是指声明一个函数，然后立即调用它。为了用局部变量。
* 于是我们声明一个 `function foo()`，然后 `foo.call()`，但是这个时候 `foo` 是全局变量（全局函数）。
* 所以我们不能给这个函数名字，使用匿名函数 `function(){}.call()` 

```
function (){}.call()
//Uncaught SyntaxError: Unexpected token (
```

* 使用 `function(){}.call()` 时候会报错（语法错误），这是因为 `JS` 引擎规定，如果 `function` 关键字出现在行首，一律解释成语句。因此，`JS` 引擎看到行首是 `function` 关键字之后，认为这一段都是函数的定义，不应该以圆括号结尾，所以就报错了。

* 解决办法：不让 `function` 出现在行首，让 `JS` 引擎将其理解成一个表达式。如下：

```
//1.将整个函数用圆括号括起来
(function(){console.log(1)}.call()); 
// 或者
(function(){console.log(1)}).call(); 

//2.函数表达式
var foo = function(){console.log(1)}.call(); 

//2.function 前面加符：+ - ! ~ 
!function (){console.log(1)}();
~function (){console.log(1)}();
+function (){console.log(1)}();
-function (){console.log(1)}();

//! ~ + - 等运算符还会和函数的返回值进行运算，有时会造成不必要的麻烦。
```

**问题：**「立即执行函数」使得`函数内部变量`无法被外部访问。这就无法满足一些特殊情况。

**解决办法：**使用「闭包」。如下：

```
//函数1
(function(){
	var person = {
		name: 'frank',
		age: 18
   }
	window.frankGrowUp = function(){
		person.age += 1
		return person.age
	}
}).call()
//或者
window.frankGrowUp = (function(){
	var person = {
		name: 'frank',
		age: 18
         }
	return function(){
		person.age += 1
		return person.age
	}
}).call()

//函数2
(function(){
	var newAge = window.frankGrowUp()
	console.log(newAge)
}).call() 

// 19
```
「闭包」使得「匿名函数」可以操作 `person`。`window.frankGrowUp` 保存了匿名函数的地址。任何地方都可以使用 `window.frankGrowUp` 操作 `person`。但是不能直接访问 `person`。

---

#### 「闭包」
##### 什么是闭包
* “函数”和“函数内部能访问到的变量（也叫环境）”的总和，就是一个闭包。
* `JavaScript`有两种作用域：全局作用域和函数作用域。函数内部可以直接读取全局变量。但是，在函数外部无法读取函数内部声明的变量。
* 换言之，如果一个函数，使用了它范围外的变量，那么‘这个函数+这个变量’就叫做闭包。

```
function f1(){
  var n = 1
  function f2(){
    console.log(n)
  }
  f2()
} 
f1()
//这段代码中，函数 f2 和变量 n 的总和就叫做闭包
```

##### 闭包的用途
1.从外部读取函数内部的变量。

	function f1(){
	  var n = 9
	  function f2(){
	    console.log(n)
	  }
	  f2()
	} 
	f1() // 9
	//这段代码中，函数f1的返回值就是函数f2，由于f2可以读取f1的内部变量，所以就可以在外部获得f1的内部变量了。


2.让这些变量始终保持在内存中。不会被垃圾机制回收。

	function f1(n) {
	  return function () {
	    return n++
	  }
	}
	var a1 = f1(1)
	a1() // 1
	a1() // 2
	a1() // 3
	//这段代码中，闭包使得内部变量记住上一次调用时的运算结果。


3.封装对象的私有属性和私有方法。

	function f1(n) {
	  return function () {
	    return n++
	  }
	}
	var a1 = f1(1)
	a1() // 1
	a1() // 2
	a1() // 3
	var a2 = f1(5)
	a2() // 5
	a2() // 6
	a2() // 7
	//这段代码中，a1 和 a2 是相互独立的，各自返回自己的私有变量。 

---

参考：[写代码啦](https://xiedaimala.com/)

