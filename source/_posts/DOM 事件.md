---
title: DOM 事件
date: 2018-01-04 15:31:21
tags:
---

#### 前面的话
`javascript`操作`CSS`称为`脚本化CSS`，而`javascript`与`HTML`的交互是通过事件实现的。事件就是文档或浏览器窗口中发生的一些特定的交互瞬间，而事件流(又叫事件传播)描述的是从页面中接收事件的顺序。

------

### DOM 事件发展
#### `DOM Level 0 事件`
	
主要分为2个：

1.标签内写 onclick 事件

	<button id="button1" onclick="console.log('hi')">A</button>

2.JS 里写 onlicke=function (){} 函数

	document.getElementById("button1").onclick = function print(){
		console.log('hi')
	}
	

#### `DOM Level 1 事件`
	
`DOM Level 1`于1998年10月1日成为 W3C 推荐标准。但是标准中并没有定义事件相关的内容，所以没有所谓的 `DOM Level 1` 事件模型。

#### `DOM Level 2 事件`

* 在`DOM Level 0 事件`的基础上弥补了一个处理程序无法同时绑定多个处理函数的缺点，允许给一个处理程序添加多个处理函数。

* 只定义了两个方法，分别用来绑定和解绑事件：
	
	`addEventListener()`   对应 IE8 中的 `attachEvent()`
	`removeEventListener()`对应 IE8 中的 `detachEvent()`

* 都有三个参数：

	参数1：事件名（不要使用 "on" 前缀）</br>
	参数2：事件触发时执行的函数</br>
	参数3：事件是否在捕获或冒泡阶段执行（第三个参数为 true，为捕获阶段；不传第三个参数或者传 false 为冒泡阶段）</br>
	
	**注意**：如果又有捕获又有冒泡，那就不区分捕获还是冒泡，按照代码顺序。


HTML

```
 <div id="grand1">
    爷爷
     <div id="parent1">
      爸爸
       <div id="child1">
        儿子
       </div>
     </div>
  </div>
```
JS

```
grand1.addEventListener('click', function fn1(){
  console.log('爷爷')
},true)//捕获阶段
parent1.addEventListener('click', function fn2(){
  console.log('爸爸')
},false)//冒泡阶段
child1.addEventListener('click', function fn3(){
  console.log('儿子')
})//冒泡阶段
//当点击‘儿子’时，打印的顺序是：爷爷、儿子、爸爸
```


#### `DOM Level 3 事件`

`DOM Level 3 事件`在`DOM Level 2 事件`的基础上添加了更多的事件类型，全部类型如下：

	UI事件，当用户与页面上的元素交互时触发，如：load、scroll
	焦点事件，当元素获得或失去焦点时触发，如：blur、focus
	鼠标事件，当用户通过鼠标在页面执行操作时触发如：dbclick、mouseup
	滚轮事件，当使用鼠标滚轮或类似设备时触发，如：mousewheel
	文本事件，当在文档中输入文本时触发，如：textInput
	键盘事件，当用户通过键盘在页面上执行操作时触发，如：keydown、keypress
	合成事件，当为IME（输入法编辑器）输入字符时触发，如：compositionstart
	变动事件，当底层DOM结构发生变化时触发，如：DOMsubtreeModified
	
	同时DOM3级事件也允许使用者自定义一些事件。
	
------	
	
### `DOM 事件流`	

事件流又称为事件传播，`DOM Level 2 事件`规定的事件流包括三个阶段：

	（1）捕获阶段：事件从 Document 节点自上而下向目标节点传播的阶段；
	（2）目标阶段：真正的目标节点正在处理事件的阶段；
	（3）冒泡阶段：事件从目标节点自上而下向 Document节点传播的阶段。
	
#### `stopPropagation()`	
在整个事件流的任何位置通过调用事件的`stopPropagation()`方法可以停止事件的传播过程	

```
grand1.addEventListener('click', function fn1(e){
  console.log('爷爷')
  e.stopPropagation()//事件不再被分派到其他节点
},true)
parent1.addEventListener('click', function fn2(){
  console.log('爸爸')
},false)
child1.addEventListener('click', function fn3(){
  console.log('儿子')
})
//当点击‘儿子’时，打印：爷爷
```
------	
