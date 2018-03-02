---
title: JS 内存
date: 2018-01-09 16:10:48
categories: JavaScript
tags:
---

### `stack`栈内存 和 `heap`堆内存

* 比如买一个 8G 的内存条
* 开机时内存分配：操作系统 512M，浏览器打开就占用 1G(100M 给`HTML`+`CSS`+`JS`+网络`HTTP`+其他)  
* `JS`最多分到 100M 内存
* `JS`引擎将内存分为代码区和数据区
* 数据区分为`Stack`（栈内存）和`Heap`（堆内存）
* 基本类型的数据直接存在`Stack`里（数字64位，字符16位）
* 复杂类型的数据是把`Heap`地址存在`Stack`里

------

### 遇到问题就画图，不要分析。

##### 举例1

	var a = {name: "tang"}
	var b = a
	b = {name: "zhao"}
	a.name = ? // "tang"
	
当执行 `var b = a` 时，内存变化如下：

<img src='https://i.loli.net/2018/01/24/5a6892882ff3c.png
'>	

当执行 `b = { name: "zhao" }` 时，内存变化如下：

<img src='https://i.loli.net/2018/01/24/5a688d4447585.png
'>
	
##### 举例2	

	var a = {name: "tang"}
	var b = a
	b.name = 'zhao'
	a.name = ? // "zhao"

当执行 `b.name = "zhao"`时，内存变化如下：

<img src='https://i.loli.net/2018/01/24/5a688d63302b0.png
'>	
	
##### 举例3
	
	var a = {name: "tang"}
	var b = a
	b = null
	a = ? // {name: "tang"}

当执行 `b = null`时，内存变化如下：

<img src='https://i.loli.net/2018/01/24/5a688d7803b75.png
'>	
	
------	

### 垃圾回收
如果一个对象没有被引用，它就是垃圾，将被回收。

##### 举例1

	var a = {name: "tang"}
	var b = {name: "zhao"}
	a = b 
	// 这时 {name: "tang"} 就是垃圾

##### 举例2

请问下面的`function(){}`会被回收吗？

	var fn = function(){}
	document.body.onclick = fn
	fn = null

当执行到 `document.body.onclick = fn`时，内存变化如下：

<img src='https://i.loli.net/2018/01/24/5a6894373204b.png
'>	

当执行到 `fn = null`时，由于`function(){}`仍然被`document`引用，故不会被回收，内存变化如下:

<img src='https://i.loli.net/2018/01/24/5a6894597cc45.png
'>

##### 举例3

下面的`function(){}`会被回收

	var fn = function(){}
	document.body.onclick = fn
	document.body.onclick = null


* 注意：IE 的 bug，使得该被标记为垃圾的没有被标记，这叫做‘内存泄漏’。
* 解决办法：页面关闭前，将所有事件 = null
	
------

### 基本类型（值）和复杂类型（引用）的区别

基本类型：`Number` `String` `undefined` `null` `Boolean` `Symbol`
复杂类型：`Object` `Function` `Array`  `Date` `RegExp`

##### 区别：基本类型的变量存的是值，复杂类型的变量存的是内存地址。

```
var n1 = new object()
var n2 = 1
```

n1 和 n2 在内存的情况如下：

<img src='https://i.loli.net/2018/01/27/5a6c49bee3322.png
'>

值得注意的是：

* 由于历史原因要求`JS`长得像`Java`，故发明了`var n = new Number(1)`这种写法。
* 但是`var n = 1`这种写法更简单，这种写法有个缺点：因为基本类型没有属性，不能使用`toString`方法。
* 于是 JS之父 发明了一个妙计，当写`n.toString()`时，声明一个临时对象`temp = new Number(n)`，将`temp.toString()`的值作为`n.toString()`的值，转换完成后就干掉`temp`，内存变化如下：

<img src='https://i.loli.net/2018/01/25/5a69a04b8bfd6.png
'>

引用《JavaScript 高级程序设计》里的话来总结：

* 为了便于操作基本类型值，`ECMAScript` 还提供了3个特殊的引用类型（也叫基本包装类型），分别是 `Boolean` `Number` `String` 。这些类型与其他引用类型相似，同时具有各自的基本类型相应的特殊行为。
* 引用类型与基本包装类型的主要区别就是对象的生存期。使用`new`操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁。

------
### 深拷贝 VS 浅拷贝
对于基本类型来说，只有深拷贝。这里我们只讲对象。

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

##### 如何实现深拷贝？（后续来补）

------

参考：[写代码啦](https://xiedaimala.com/)

