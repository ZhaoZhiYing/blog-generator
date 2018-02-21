---
title: JS 数组
date: 2018-02-20 17:13:10
tags:
---
#### 什么是数组
人类理解：数组就是数据的有序集合（每个值的位置都有索引（从0开始））
JS理解：数据就是原型链中有 `Array.prototype` 的对象。

---

#### 创建数组
1.使用 `Array` 构造函数。
  
	var arr = new Array(8) //创建 length 为 8 的数组。
	var arr = new Array('red', 'blue', 'green') //创建了包含3个字符串的数组
	
	//new 操作符可省略，上面代码同等于下：
	var arr = Array(8) 
	var arr = Array('red', 'blue', 'green') 
	
2.数组字面量	
	
	//创建了包含3个字符串的数组
	var arr = ['red', 'blue', 'green']
	
	//除了在定义时赋值，数组也可以先定义后赋值。
	var arr = []
	arr[0] = 'a'
	
	//数组可以保存任何类型的数据。
	var arr = [
	  {a: 1},
	  [1, 2, 3],
	  function() {return true;}
	]
	arr[0] // Object {a: 1}
	
	//如果数组的元素还是数组，就形成了多维数组。
	var a = [[1, 2], [3, 4]]
	a[0][1] // 2 
	a[1][1] // 4

---

#### `length` 属性
数组的`length`属性是可写的，如下：

	var arr = ['red', 'blue', 'green']
	arr.length = 4 
	arr[3] // undefined 

	var arr = ['red', 'blue', 'green']
	arr.length = 2 // 这里删除了 arr[2]
	arr[2] // undefined 
	
	var arr = ['red', 'blue', 'green']
	arr[3] = 'gray' //这里增加了一项
	arr.length // 4

---

#### 检测数组
##### `instanceof` 和 `isArray`

`instanceof`语法
	
	object instanceof constructor
	//object 要检测的对象
	//constructor 某个构造函数
	
	//如下	
	var obj = []
	obj instanceof Array //true
	
`isArray`语法
	
	Array.isArray(obj) //obj 需要检测的值
	
	//如下
	var obj = Array(1,2,3)
	Array.isArray(obj) //true
	
	Array.isArray([1,2,3]) //true

>在浏览器中，我们的脚本可能需要在多个窗口之间进行交互。多个窗口意味着多个全局环境，不同的全局环境拥有不同的全局对象，从而拥有不同的内置类型构造函数。

这时当检测`Array`实例时，`Array.isArray` 优于 `instanceof`,因为`Array.isArray`能检测`iframes`。

示例
	
	var iframe = document.createElement('iframe')
	document.body.appendChild(iframe)
	
	arr1 = window.frames[window.frames.length-1].Array
	var arr2 = new arr1(1,2,3) // [1,2,3]
	
	
	Array.isArray(arr) // true
	arr instanceof Array // false

---

#### 伪数组（类数组）
* 有 0,1,2,3,4,5...n,length 这些 key 的对象
* 原型链中没有 `Array.prototype`。或者说没有 `push` 方法。

比如函数的`argument`参数，还有像调用`getElementsByTagName` `document.childNodes`之类的，它们都返回`NodeList`对象都属于伪数组。

伪数组转成真数组方法 
    
    var arr = Array.prototype.slice.call(fakeArray)
    //fakeArray 表示一个伪数组
    
示例

	var fakeArray = {0:'a',1:'b',length:2} //伪数组
	var arr1 = Array.prototype.slice.call(fakeArray)
	arr1[0] //"a"	
	//或者
	var arr2 = [].slice.call(fakeArray) 
	arr2[0] //"a"

---