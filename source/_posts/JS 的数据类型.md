---
title: JS 的数据类型
date: 2017-12-28 11:53:47
tags:
---
JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有七种。

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

#### 1.number 数值

	(1) 十进制: 整数小数(1, 1.1, .1)
               科学计数法：12e2 // 1200
				   	     12e-2 // 0.12
	(2) 二进制：0b开头
	(3) 八进制：0开头
	(4) 十六进制：0x开头
-------

#### 2.string（字符串）
 
	(1) 用 ‘’或“”引起来
	(2)转义符：\（同命令行回车：\ ）
	(3)连接符：+（+ 写在每行结尾，适用于多行字符串）
	(4)反引号：`（`写在开头结尾，适用于多行字符串，每行含有一个回车）
-------

#### 3.boolean（布尔值）

	true（真）和false（假）两个特定值
	
-------

#### 4.undefined

	表示“未定义”或不存在
         
-------

#### 5.null

	表示无值，即此处的值就是“无”的状态。

##### `null`和`udefined`区别

	null：表示空值，即该处的值现在为空。调用函数时，某个参数未设置任何值，这时就可以传入null。
	undefined：表示"缺少值"，就是此处应该有一个值，但是还没有定义。
	1.语法：如果一个变量没有赋值，就是 undefined
	2.惯例：如果有一个对象object，但是现在不想赋值，那就给一个 null（推荐）
	       如果有一个非对象，不想赋值，推荐初始化成 undefined 
-------

#### 6.symbol（符号）
Symbol 可以创建一个独一无二的值（但并不是字符串）。

	var x = Symbol('a')
	var y = Symbol('a')
	x !== y // true
 
-------

#### 7.object（对象）

对象就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合。

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
             
##### 检查变量是否声明（in运算符）

	var o = { p: 1 };
	'p' in o // true (注意，检查的是键名，不是键值)
	
##### 查看所有属性（Object.keys）	

	var o = {
	  key1: 1,
	  key2: 2
	};
	
	Object.keys(o);
	// ['key1', 'key2']
	
##### delete命令

	//无value无key
	var person = {
		'name': 'zhaozhao'
 	} 
 	delete person['name']
 	person.name //undefined
 	'name' in person //false
 	
 	//无value 有key
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
参考：

[阮一峰的《JavaScript 标准参考教程》](http://javascript.ruanyifeng.com/grammar/function.html)

[写代码啦] (https://xiedaimala.com/)