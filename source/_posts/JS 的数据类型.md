---
title: JS 的数据类型
date: 2017-12-28 11:53:47
tags:
---
`JavaScript`语言的每一个值，都属于某一种数据类型。`JavaScript`的数据类型，共有七种。

---
### 数据类型

##### 六种基本类型

	number 数值
	string 字符串
	boolean 布尔值
	undefined 
	null
	symbol 符号
	
##### 一种复杂类型

	object 对象
	
	下面两种也属于对象：
	* 数组（array）
	* 函数（function）

-------

#### 1.`number`(数值)

	(1) 十进制: 整数小数(1, 1.1, .1)
               科学计数法：12e2 // 1200
				   	     12e-2 // 0.12
	(2) 二进制：0b开头
	(3) 八进制：0开头
	(4) 十六进制：0x开头
	
-------

#### 2.`string`(字符串）
 
	(1) 用 '' 或 "" 引起来
	(2)转义符：\（同命令行回车：\ ）
	(3)连接符：+（+ 写在每行结尾，适用于多行字符串）
	(4)反引号：`（`写在开头结尾，适用于多行字符串，每行含有一个回车）
-------

#### 3.`boolean`(布尔值）

	true（真）和 false（假）两个特定值
	
-------

#### 4.`undefined`
在使用`var`声明变量但未对其初始化时，这个变量的值就是`undefined`

	var message;
	message === undefined; // true

对为初始化和未声明的变量执行`typeof`操作符都返回`undefined`值
	
	var message; //message 声明后默认取得了 undefined 值
	//var age  // age 未声明
	
	typeof message //undefined	
	typeof age //undefined		
         
-------

#### 5.`null`
`null`表示一个空对象指针

	typrof null //"object"
	
如果定义的变量准备将来用来保存对象，那么最好将该变量初始化为`null`。

	var message = null	
	
`undefined`派生自`null`，`ECMA-262`规定它们的相等性测试(==)返回`true`

	undefined == null //true


#### 6.`symbol`(符号）
`symbol`可以创建一个独一无二的值（但并不是字符串）。

	var x = Symbol('a')
	var y = Symbol('a')
	x !== y // true
 
-------

#### 7.`object`(对象）

对象就是一组“键值对”`key-value`的集合，是一种无序的复合数据集合。

	var person = {
		'name': 'zhaozhao', //键值是字符串
		'Age': 18，//键值是数值，
		'married': true,  //键值是布尔值
		'children': { name: 'xxx', age: 1,} //键值是对象
		''：'hh', //键名是空字符串，person[''] = hh
		'p': function (x) {return 2 * x;}//键值是函数，也叫做方法
 	} 
 	person['name']//zhaozhao
 	
   
##### 键名和键值
    
	* 对象的所有键名都是字符串，所以加不加引号都可以。
	* 如果键名不符合标识名的条件（比如第一个字符为数字，或者含有空格或运算符），也不是数字，则必须加上引号，否则会报错。   
	* 对象的每一个“键名”又称为“属性”。
	* 如果一个属性的“键值”为函数，通常把这个属性称为“方法”，它可以像函数那样调用。 
    
##### 读取属性

	* 一种是使用点运算符：person.name（键名符合标识名条件）
	* 一种是使用方括号运算符：person['name']//zhaozhao
	* 数值只能用方括号运算符：obj[0xFF]
	* 数字键可以不加引号，因为会被当作字符串处理：o[0.7]
             
##### 检查变量是否声明(`in`运算符）

	var o = { p: 1 };
	'p' in o // true (注意，检查的是键名，不是键值)
	
##### 查看所有属性`Object.keys`

	var o = {
	  key1: 1,
	  key2: 2
	};
	
	Object.keys(o);
	// ['key1', 'key2']
	
##### `delete`命令

	//无 value 无 key
	var person = {
		'name': 'zhaozhao'
 	} 
 	delete person['name']
 	person.name //undefined
 	'name' in person //false
 	
 	//无 value 有 key
 	var person = {
		'name': 'zhaozhao'
 	} 
 	person.name = undefined
 	'name' in person //true
 	
##### `for…in`循环

	//遍历键值
	var person = {
		'name': 'zhaozhao',
		'age': 18,
 	} 	
 	for(var key in person){
 		console.log(person[key])
 	}
 	//zhaozhao
	//18
	
	//遍历键名
	for(var key in person){
 		console.log(key)
 	}
	//name
	//age

-------
### 检测数据类型
##### 检测基本类型`typeof`
* 要检测一个变量是字符串、数值、布尔值还是`undefined`，用`typeof`操作符。
* `typeof`操作符返回一个字符串，指示未经计算的操作数的类型。
* 语法：`typeof operand`，`operand`是一个表达式，表示对象或原始值，其类型将被返回。

```
var s = 'message'
typeof s //"string"
```

##### 检测对象`instanceof`
* 如果变量的值是一个对象或`null`，则用`instanceof`操作符
* 语法：`object instanceof constructor`，返回一个布尔值。
* `instanceof`运算符用来检测`constructor.prototype`是否存在于参数 `object`的原型链上。

```
var obj = {}
obj instanceof Object //true
obj instanceof Array //false
```

##### 检测对象 `toString()` 
为了每个对象都能通过 `Object.prototype.toString()` 来检测，需要以 `Function.prototype.call()` 或者 `Function.prototype.apply()` 的形式来调用，传递要检查的对象作为第一个参数。

	var toString = Object.prototype.toString
	
	toString.call(new Date(1995, 11, 17)) // "[object Date]"
	toString.call('1') // "[object String]"
	toString.call(1) // "[object Number]"
	toString.call(Math) // "[object Math]"

-------

参考：

[写代码啦] (https://xiedaimala.com/)