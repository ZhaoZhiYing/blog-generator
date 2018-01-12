---
title: call、apply、bind 的用法区别
date: 2018-01-03 22:02:33
tags:
---
#### `call`
`call`是函数的正常调用方式，并指定上下文`this`。

#### `apply`
`apply`的作用和`call`一样，只是在调用的时候，传参数的方式不同。
`apply`接受的是数组参数，`call`接受的是连续参数。如下代码：

	function add(a,b){
	    return a+b;
	}
	add.call(add, 5, 3); //8
	add.apply(add, [5, 3]); //8
	
#### `bind`
`bind`接受的参数跟`call`一致，只是`bind`不会立即调用，它会生成一个新的函数，你想什么时候调就什么时候调。如下代码：

	function add(a, b){
	    return a+b;
	}
	var foo1 = add.bind(add, 5,3); 
	foo1(); //8
	var foo1 = add.bind(add, 5,3); 
	foo1(); //8