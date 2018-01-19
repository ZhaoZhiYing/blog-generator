---
title: JS 函数
date: 2017-12-29 19:14:26
tags:
---
#### 什么是函数

函数就是一段可以反复调用的代码块。

-------
#### 函数的5种声明
   
##### 1.function命令(函数声明)
	function print(s) {   //print是函数名，也叫标识符
	console.log(s);   //这是函数体
	} //函数的声明在结尾的大括号后面不用加分号	
##### 2.函数表达式(匿名)
	var print = function (s) { //这个匿名函数又称函数表达式
	console.log(s); 
	 }; //函数的表达式需要在语句的结尾加上分号，表示语句结束	 
注意：采用函数表达式声明函数时，function命令后面不带有函数名。
      如果加上函数名，该函数名只在函数体内部有效，在函数体外部无效。
      
	var print = function x(){
	  console.log(typeof x);
	};
	x// ReferenceError: x is not defined
	print()// function	
	
##### 3.函数表达式(具名)
	var print = function  f(s) { 
	  console.log(s); 
	};	
	
##### 4.Function构造函数（一般不用）(window.Function函数对象)
	var add = new Function(
	  'x',
	  'y',
	  'return x + y'
	);
	// 等同于
	function add(x, y) {
	  return x + y;
	} 
	
##### 5.箭头函数(匿名) (x , y) => { return x + y }

	(参数1, 参数2, …, 参数N) => {函数声明}
	(参数1, 参数2, …, 参数N) => 表达式（单一）
	//相当于：(参数1, 参数2, …, 参数N) =>{ return表达式}
	
	// 当只有一个参数时，圆括号是可选的：
	(单一参数) => {函数声明}
	单一参数 => {函数声明}
	
	// 没有参数的函数应该写成一对圆括号。
	() => {函数声明}

##### `function print(){}`和`var s = function print(){}`区别

	不一致性
	输入console.log(print)时：
	function print(){}可以访问，var s = function print(){}不能访问
	
-------

#### 函数的属性和方法
##### name属性
`name`属性返回紧跟在`function`关键字之后的那个函数名。

	function f1() {}; f1.name // 'f1'
	var f2 = function () {}; f2.name // ‘f2’
	var f3 = function f4() {}; f3.name // ‘f4’
	f5 = new Function('x', 'y','return x + y’){};   
	f5.name//‘anonymous’ (匿名) 
  
##### length属性
`length`属性返回函数预先定义的参数个数。

-------

#### 函数作用域
##### 定义
作用域（scope）指的是变量存在的范围。Javascript 只有两种作用域：

	(1)全局作用域：变量在整个程序中一直存在，所有地方都可以读取；
	     在函数外部声明的变量就是全局变量。
	     
	(2)函数作用域：在函数内部定义的变量，外部无法读取。

注意：函数内部定义的变量，会在该作用域内覆盖同名全局变量。
     对于var命令来说，局部变量只能在函数内部声明，在其他区块中声明，一	  律都是全局变量。
       
-------  
#### 函数内部的变量提升
var命令声明的变量，不管在什么位置，变量声明都会被提升到函数体的头部。

	function foo(x) {
	  if (x > 100) {
	    var tmp = x - 100; //会升到函数体头部
	  }
	}
	
-------

#### `return`
每个函数都有`return`
如果你不写`return`，就相当于写了`return undefined`
	
-------

#### 递归
递归函数是一个直接或间接调用函数自身的嵌套型函数。

	function fn(num) {
	  if (num === 0) return 0;
	  if (num === 1) return 1;
	  return fn(num - 2) + fn(num - 1);
	}
	fn(6) // 8


-------

#### 闭包
##### 什么是闭包
“函数”和“函数内部能访问到的变量（也叫环境）”的总和，就是一个闭包。
`JavaScript`有两种作用域：全局作用域和函数作用域。函数内部可以直接读取全局变量。但是，在函数外部无法读取函数内部声明的变量。换言之，如果一个函数，使用了它范围外的变量，那么‘这个函数+这个变量’就叫做闭包。

	function f1() {
	  var n = 1;
	  function f2() {
	    console.log(n);
	  }
	  return f2;
	} 
	//这段代码中，函数 f2 和变量 n 的总和就叫做闭包

##### 闭包的用途
1.从外部读取函数内部的变量。

	function f1() {
	  var n = 9;
	  function f2() {
	    console.log(n);
	  }
	  return f2;
	} 
	var result = f1();
	result(); // 9
	//这段代码中，函数f1的返回值就是函数f2，由于f2可以读取f1的内部变量，所以就可以在外部获得f1的内部变量了。

2.让这些变量始终保持在内存中。不会被垃圾机制回收。

	function f1(n) {
	  return function () {
	    return n++;
	  };
	}
	var a1 = f1(1);
	a1() // 1
	a1() // 2
	a1() // 3
	//这段代码中，闭包使得内部变量记住上一次调用时的运算结果。

3.封装对象的私有属性和私有方法。

	function f1(n) {
	  return function () {
	    return n++;
	  };
	}
	var a1 = f1(1);
	a1() // 1
	a1() // 2
	a1() // 3
	var a2 = f1(5);
	a2() // 5
	a2() // 6
	a2() // 7
	//这段代码中，a1 和 a2 是相互独立的，各自返回自己的私有变量。
-------

#### 调用函数
##### `call`
`call`是函数的正常调用方式，并指定上下文`this`。

##### `apply`
`apply`的作用和`call`一样，只是在调用的时候，传参数的方式不同。
`apply`接受的是数组参数，`call`接受的是连续参数。如下代码：

```
function add(a,b){
    return a+b;
}
add.call(add, 5, 3); //8
add.apply(add, [5, 3]); //8
```	
	
##### `bind`
bind 接受的参数跟 call 一致，只是 bind 不会立即调用，它会生成一个新的函数，你想什么时候调就什么时候调。如下代码：

```	
function add(a, b){
    return a+b;
}
var foo1 = add.bind(add, 5,3); 
foo1(); //8
var foo1 = add.bind(add, 5,3); 
foo1(); //8
```	    
-------
#### `this`和`arguments`

`this`是函数的第一个参数（且必须是对象）,`arguments`是函数的第二个参数（包装成一个数组[]）<br/>

普通模式：如果`this`是`undefined`或`null`，浏览器会把`this`变成`window`<br/>

严格模式：第一个参数是什么，浏览器会把`this`变成什么.<br/>
	
	  function f(){
      console.log(this)
      console.log(arguments)
	  }
	  f.call() // window
	  f.call({name:'frank'}) // {name: 'frank'}, []
	  f.call({name:'frank'},1) // {name: 'frank'}, [1]
	  f.call({name:'frank'},1,2) // {name: 'frank'}, [1,2]
  
 `this`为什么必须是对象，因为`this`就是函数与对象之间的羁绊。

      var person = {
          name: 'frank',
          sayHi: function(person){
              console.log('Hi, I am' + person.name)
          },
          sayBye: function(person){
              console.log('Bye, I am' + person.name)
          },
          say: function(person, word){
              console.log(word + ', I am' + person.name)
          }
      }
      person.sayHi(person)
      person.sayBye(person)
      person.say(person, 'How are you')

      // 能不能变成 
      person.sayHi()
      person.sayBye()
      person.say('How are you')

      // 那么源代码就要改了
      var person = {
          name: 'frank',
          sayHi: function(){
              console.log('Hi, I am' + this.name)
          },
          sayBye: function(){
              console.log('Bye, I am' + this.name)
          },
          say: function(word){
              console.log(word + ', I am' + this.name)
          }
      }
      // 如果你不想吃语法糖
      person.sayHi.call(person)
      person.sayBye.call(person)
      person.say.call(person, 'How are you')

      // 还是回到那句话：this 是 call 的第一个参数
      // this 是参数，所以，只有在调用的时候才能确定
      person.sayHi.call({name:'haha'})  // 这时 sayHi 里面的 this 就不是 person 了
      // this 真的很不靠谱

      // 新手疑惑的两种写法
      var fn = person.sayHi
      person.sayHi() // this === person
      fn()  // this === window
	
##### `this`的历史原因
要长得像`Java`，让`Java`程序员来学`JS`，但是他们发现`this`多余，就有了 `use strict` 

-------	

##### `Call Stack`先入后出
`call stack`调用堆栈，调用堆栈是一个方法列表，按调用顺序保存所有在运行期被调用的方法。

	function a(){
		console.log(‘a’)
		return a
	}
	a.call() 
当调用时，```a.call()```会被记在 call stack 里。接着 ```console.log(‘a’)``` 记在 call stack 里。```return a``` 到这一步时```console.log(‘a’)```会存在```a.call()```里，最后```a.call()```退出

-------
参考：

阮一峰的《JavaScript 标准参考教程》<http://javascript.ruanyifeng.com/grammar/function.html>

写代码啦 <https://xiedaimala.com/>
