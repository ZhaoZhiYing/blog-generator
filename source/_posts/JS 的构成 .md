---
title: JS 的构成  
date: 2017-12-21 21:06:21
categories: JavaScript
tags:
---

### `JavaScript`是什么？
`JavaScript`是一种轻量的、解释性的、面向对象的头等函数语言，其最广为人知的应用是作为网页的脚本语言，但同时它也在很多非浏览器环境下使用。`JS`是一种动态的基于原型和多范式的脚本语言，支持面向对象、命令式和函数式的编程风格。

------

### `JavaScript`的三大组成部分
**`ECMAScript`**

```
* ECMAScript 是一种开放的、国际上广为接受的脚本语言规范。由欧洲计算机制造商协会制定和发布。 Web 浏览器对于 ECMAScript 来说只是一个宿主环境，但它并不是唯一的宿主环境。	
* ECMAScript 是由 ECMA-262 定义， ECMA-262 标准规范了一种脚本语言实现应该包含的内容（语法、数据类型、语句、关键字、保留字、操作符以及对象）
* ECMAScript 和 JavaScript 的关系是，前者是后者的规格，后者是前者的一种实现。在日常场合，这两个词是可以互换的。
```
		
**`DOM`**

```
* DOM (Document Object Model 文档对象模型）是 W3C 组织制定的一套用于访问和操作 XML ( HTML 是 XML 的衍生品)文档的标准。
* 它给文档提供了一种结构化的表示方法，并定义了一种方式可以使从程序中对该结构进行访问，从而改变文档的结构，样式和内容。
* DOM 将文档解析为一个由节点和对象（包含属性和方法的对象）组成的结构集合。
```

**`BOM`**

```
* BOM（Browser Object Model浏览器对象模型）提供与浏览器交互的方法和接口，可以访问和操作浏览器窗口。	
* 由于 BOM 没有相关标准，每个浏览器都有其自己对 BOM 的实现方式。BOM 有窗口对象、导航对象等一些实际上已经默认的标准，但对于这些对象和其它一些对象，每个浏览器都定义了自己的属性和方式。
	
例如：弹出新的浏览器窗口，移动、改变和关闭浏览器窗口，提供详细的网络浏览器信息（navigator），详细的页面信息（location），详细的用户屏幕分辨率的信息（screen），对 cookies 的支持等等。BOM 作为 JavaScript 的一部分并没有相关标准的支持，每一个浏览器都有自己的实现，虽然有一些非事实的标准，但还是给开发者带来一定的麻烦。
```
	
------

参考：

阮一峰的《JavaScript 标准参考教程》<http://javascript.ruanyifeng.com/introduction/history.html#toc1>

MDN <https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model/Introduction>	