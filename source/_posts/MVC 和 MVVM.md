---
title: MVC 和 MVVM
date: 2018-02-02 22:32:28
categories: JavaScript
tags:
---


#### 模块化

不同功能的代码放在各自的块里，模块间各自独立，互不影响。

参考：[阮一峰-模块的写法](http://www.ruanyifeng.com/blog/2012/10/javascript_module.html)

---

#### `MVC` 是什么？

`MVC`（`Model View Controller` 模型-视图-控制）指一种代码组织形式。它将代码分成三层：

	1. Model 模型：也就是程序需要操作的数据或信息。 MVC 核心。
	2. View 视图：提供给用户操作的界面。
	3. Controller 控制层：它负责根据用户从"视图层"输入的指令，选取"数据层"中的数据，然后对其进行相应的操作，产生最终结果。

#### `MVC`控制流程	
 
	1. 用户请求时触发 View ，View 会通知 Controller 。
	2. 于是 Controller 调用 Model ，Model 向 server 发送请求。
	3. server 响应后返回数据给 Model ，Model 再将数据返回给 Controller ，Controller 拿到数据后更新 View 。

#### `MVC` 三个对象分别有哪些重要属性和方法?

`View`
	
	 * el
	 * template
	 * render()
	
`Model`

	 * data
	 * fetch()
	 * save()

`Controller`  

	 * init()
	 * bindEvents (绑定事件)
 
---

#### `MVVM`

`MVC` 向 `MVVM` 的演变过程

	* 如果有多个文件，需要重复写 MVC。
	* 解决方法：利用构造函数和原型改写 MVC。
	* 引入 Vue 后（代替 View），可以实现双向绑定，变成自动化的 MVC。也叫做 MVVM。

---	










