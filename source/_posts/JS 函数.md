---
title: JS 函数
date: 2017-12-29 19:14:26
categories: JavaScript
tags:
---
#### 什么是函数

函数就是一段可以反复调用的代码块。

-------
#### 函数的几种声明
   
##### 1.函数声明（`function`命令）

	function print(s){ //print是函数名，也叫标识符
		console.log(s) //这是函数体
	} //函数的声明在结尾的大括号后面不用加分号	

	
##### 2.函数表达式
	
	//采用函数表达式声明函数时， function 命令后面不带有函数名。
	var print = function (s){ 
		console.log(s)
	}
	
	//如果加上函数名，该函数名只在函数体内部有效，在函数体外部无效。
	var print = function f(){
	  console.log(typeof f)
	}
	f// ReferenceError: f is not defined
	print()// function	

##### 3.`Function` 构造函数
	var add = new Function(
	  'x',
	  'y',
	  'return x + y'
	)
	// 等同于
	function add(x, y) {
	  return x + y
	} 

	
##### 4.箭头函数(匿名)`(x , y) => { return x + y }`
引入箭头函数有两个方面的作用：更简短的函数并且不绑定自己的`this`

	(参数1, 参数2, …, 参数N) => {函数声明}
	(参数1, 参数2, …, 参数N) => 表达式（单一）
	//相当于：(参数1, 参数2, …, 参数N) =>{ return表达式}
		
	// 当只有一个参数时，圆括号是可选的：
	(单一参数) => {函数声明}
	单一参数 => {函数声明}
		
	// 没有参数的函数应该写成一对圆括号。
	() => {函数声明}

-------

#### 函数的参数
`ECMAScript` 函数中的参数在内部是用一个类似数组的`arguments`对象来表示的，在函数体内，可以通过 `arguments`对象来访问这个参数数组，从而获取传递给函数的每一个参数。

	function add(){
		return arguments[0] + arguments[1]
	}
	
	add(2,3,4)//5

---

#### 函数的属性
##### `name`属性
`name`属性返回紧跟在`function`关键字之后的那个函数名。

	function f1() {}; f1.name // 'f1'
	var f2 = function () {}; f2.name // ‘f2’
	var f3 = function f4() {}; f3.name // ‘f4’
	f5 = new Function('x', 'y','return x + y’){}  
	f5.name//‘anonymous’ (匿名) 

  
##### `length`属性
`length`属性返回函数预先定义的参数个数。

--- 

#### 函数作用域
##### 定义
作用域`scope`指的是变量存在的范围。`Javascript` 只有两种作用域：

	(1)全局作用域：变量在整个程序中一直存在，所有地方都可以读取；在函数外部声明的变量就是全局变量。
	     
	(2)函数作用域：在函数内部定义的变量，外部无法读取。
	
	//函数内部定义的变量，会在该作用域内覆盖同名全局变量。
	//对于var命令来说，局部变量只能在函数内部声明，在其他区块中声明，一律都是全局变量。

       
-------  

#### 函数内部的变量提升
`var`命令声明的变量，不管在什么位置，变量声明都会被提升到函数体的头部。

	function foo(x){
	  if (x > 100){
	    var tmp = x - 100 //会升到函数体头部
	  }
	}

	
-------

#### `return`
* 每个函数都有`return`。
* 如果你不写`return`，就相当于写了`return undefined`。

作用：返回一个值给函数，并且结束函数执行。

	function foo(a,b){      
		return a + b;
	} 
	foo(2,3) //5
	

	function foo(){
		console.log(1);       
		return;
		console.log(2);
	} 
	foo() //1

	
-------

#### 递归
递归函数是一个直接或间接调用函数自身的嵌套型函数。

	function fn(num){
	  if (num === 0) return 0
	  if (num === 1) return 1
	  return fn(num - 2) + fn(num - 1)
	}
	fn(6) // 8


-------

#### 调用函数
##### `call`
`call`是函数的正常调用方式，并指定上下文`this`。

##### `apply`
`apply`的作用和`call`一样，只是在调用的时候，传参数的方式不同。
`apply`接受的是数组参数，`call`接受的是连续参数。如下代码：


	function add(a,b){
	    return a+b
	}
	add.call(add, 5, 3) //8
	add.apply(add, [5, 3]) //8

	
##### `bind`
`bind` 接受的参数跟 `call` 一致，只是 `bind` 不会立即调用，它会生成一个新的函数，你想什么时候调就什么时候调。如下代码：

	function add(a, b){
	    return a+b;
	}
	var foo1 = add.bind(add, 5,3)
	foo1() //8
	var foo1 = add.bind(add, 5,3) 
	foo1() //8
 
   
-------

##### `eval()`
 * `eval()`函数会将传入的字符串当做`JavaScript`代码进行执行。
 * 语法：`eval(string)`
 * 如果字符串表示的是表达式，`eval()`会对表达式进行求值。
 * 如果参数表示一个或多个`JavaScript语句`， 那么`eval()`就会执行这些语句。
 
```
eval('var a = 1;')
a // 1
```

-------


参考：[写代码啦] (https://xiedaimala.com/)
