---
title: 深拷贝 VS 浅拷贝
date: 2018-03-30 18:32:17
categories: JavaScript
tags:
---


>对于基本类型来说，只有深拷贝。这里我们只讲对象。

##### 深拷贝
对于对象来说，深拷贝是指在`栈内存`中新增一个指针，并且在`堆内存`中申请了一个新的内存。

	var a = {name:"tang"}
	var b = a 
	b.name = "zhao";  
	//a.name = "tang"

<img src='https://i.loli.net/2018/01/24/5a68936065884.png
'>	
	
##### 浅拷贝
对于对象来说，浅拷贝只是在`栈内存`中新增一个指针指向原有的内存，只是拷贝了内存地址（`Heap`地址）。

	var a = {name:"tang"}
	var b = a
	b.name = "zhao"
	//a.name = "zhao"
	
<img src='https://i.loli.net/2018/01/24/5a6892b18918c.png
'>	

---

#### 如何实现深拷贝？

##### `JSON` 实现深拷贝
	
	var obj = {}
	var cloneObj = JSON.parse(JSON.stringify(obj))
	
缺点

	JSON 不支持函数、引用、undefined、RegExp、Date等。
	
##### 递归拷贝

	function deepClone(object){
		var object2
		if(!(object instanceof Object)){
			return object
		}else if(object instanceof Array){
			object2 = []
		}else if(object instanceof Function){
			object2 = eval(object.toString())
		}else if(object instanceof Object){
			object2 = {}
		}
		for(let key in object){
			object2[key] = clone(object[key])
		}
		return object2
	}
	
	var obj = {0:1, 1:5, 2:2, 3:1}
	var arr = [2, 2, 3, 4, 4, 6, 6]
	
	var newObj = deepClone(obj)
	var newArr = deepClone(arr)
	
	newObj //{0:1, 1:5, 2:2, 3:1}
	newArr //[2, 2, 3, 4, 4, 6, 6]
	
---	