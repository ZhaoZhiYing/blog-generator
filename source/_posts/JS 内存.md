---
title: JS 内存
date: 2018-01-23 15:27:32
tags:
---

#### `stack`栈内存 和 `heap`堆内存

* 比如买一个 8G 的内存条
* 开机时内存分配：操作系统 512M，浏览器打开就占用 1G(100M 给`HTML`+`CSS`+`JS`+网络`HTTP`+其他)  
* `JS`最多分到 100M 内存
* `JS`引擎将内存分为代码区和数据区
* 数据区分为`Stack`（栈内存）和`Heap`（堆内存）
* 基本类型的数据直接存在`Stack`里（数字64位，字符16位）
* 复杂类型（引用类型）的数据是把`Heap`地址存在`Stack`里

基本类型：`Number` `String` `undefined` `null` `Boolean` `Symbol`<br/>
引用类型：`Object` `Array` `Date` `RegExp` `Function`

------

#### 遇到问题就画图，不要分析。

##### 举例1

	var a = {name: "tang"}
	var b = a
	b = {name: "zhao"}
	a.name = ? // "tang"
	
当执行 `var b = a` 时，内存的变化如下：

<img src='https://i.loli.net/2018/01/24/5a6892882ff3c.png
'>	

当执行 `b = { name: "zhao" }` 时，内存的变化如下：

<img src='https://i.loli.net/2018/01/24/5a688d4447585.png
'>
	
##### 举例2	

	var a = {name: "tang"}
	var b = a
	b.name = 'zhao'
	a.name = ? // "zhao"

当执行 `b.name = "zhao"`时，内存的变化如下：

<img src='https://i.loli.net/2018/01/24/5a688d63302b0.png
'>	
	
##### 举例3
	
	var a = {name: "tang"}
	var b = a
	b = null
	a = ? // {name: "tang"}

当执行 `b = null`时，内存的变化如下：

<img src='https://i.loli.net/2018/01/24/5a688d7803b75.png
'>	
	
------	

#### 垃圾回收
* 如果一个对象没有被引用，它就是垃圾，将被回收。

##### 举例1
```
var a = {name: "tang"}
var b = {name: "zhao"}
a = b 
// 这时 {name: "tang"} 就是垃圾
```
##### 举例2
请问下面的`function(){}`会被回收吗？

```
var fn = function(){}
document.body.onclick = fn
fn = null
```	
当执行到 `document.body.onclick = fn`时，内存的变化如下：

<img src='https://i.loli.net/2018/01/24/5a6894373204b.png
'>	

当执行到 `fn = null`时，由于`function(){}`仍然被`document`引用，故不会被回收，如下。

<img src='https://i.loli.net/2018/01/24/5a6894597cc45.png
'>

##### 举例3
下面的`function(){}`会被回收

```
var fn = function(){}
document.body.onclick = fn
document.body.onclick = null
```
* 注意：IE 的 bug，使得该被标记为垃圾的没有被标记，这叫做‘内存泄漏’。
* 解决办法：页面关闭前，将所有事件 = null
	
------

#### 深拷贝 VS 浅拷贝

深拷贝

	var a = {name:"tang"}
	var b = a 
	b.name = "zhao";  
	//a.name = "tang"

<img src='https://i.loli.net/2018/01/24/5a68936065884.png
'>	
	
浅拷贝

	var a = {name:"tang"}
	var b = a
	b.name = "zhao"
	//a.name = "zhao"
	
<img src='https://i.loli.net/2018/01/24/5a6892b18918c.png
'>	

------

参考：[写代码啦] (https://xiedaimala.com/)


