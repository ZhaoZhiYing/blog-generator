---
title:  HTML 标签
date: 2017-10-24 10:32:19
tags:
---


>常见标签：a、form（表格）、input（表单，包含输入框和提交按钮）、button、h1、p、ul、ol、small、strong、div、span、kbd(键盘按键)、video（视频）、audio（音频）、svg（不规则图形）
>
>注意：除了`div`和`span`，其他标签都有默认样式

### iframe标签
在当前页面嵌套一个页面（可替换标签）(支持相对路径)

	1.默认宽100px高50px
	2.默认有难看的border，所以默认写frameborder=0
	3.name属性需结合a标签使用，否则无意义(name可结合a标签的target指定嵌套网页打开窗口)       
	4.src指定路径（可以是相对路径）


### `<a>`标签
##### `target`属性
   
该属性指定在何处显示链接的资源。

	* _self    默认属性。当前页面加载。
	* _blank   新窗口打开
	* _parent  父级页面打开。如果没有，同_self。
	* _top     顶级页面加载。如果没有，同_self。 
	
##### `<href>`属性

必需属性。该属性规定链接的目标地址。

	* href="//qq.com" 无协议地址
	* href="#xxx" 锚点#，不发起请求
	* href="?name=qq" 发起请求
	* href="./xxx.html" 相对路径 
	* href="javascript:;" 让a标签不跳转
	* href="javascript:alert(1)" 执行一段代码
	* href="http://write.blog.csdn.net" 绝对 URL ，指向另一个站点
	* a href=""；刷新页面
	* href="#top" 返回到页面顶部
	* href="#" 返回到页面顶部

如何实现浏览器以下载形式接收请求，而不是显示页面？

	1. a 标签里加 download
	   <a href="/images/logo.png" download="logo">
	
	2. Content-type: application/octet-stream

### `<form>`标签
跳转页面（主要使用POST 请求，参数放到第四部分from datas）（使用GET请求时，参数默认放到查询参数）

	 1.如果 form 表单里没有提交按钮，就无法提交
	 2.form 标签主要用来发起post请求
	 3.name 属性值显示在第四部分
	 4.target 属性同 a 标签

##### 注意：a标签和form标签都是用来发请求，a标签是get，form标签是post

### `<input>`标签
input没有子元素，button有子元素

    type属性 
	1.如果一个form只有一个按钮button，没写type，自动升级为sunmit可提交。
	  submit是唯一能确定type能不能提交的按钮，button只是一个普通按钮。
	2.checkbox: 单选框
	3.radio: 复选框
	
### `<label>`标签
关联input（label的for值和input的name值一样，用于选项）（更聪明的写法是：用label标签包裹input标签，不需要for和name）
### `<select>`标签
下拉列表
### `<textarea>`标签
输入多行文本
1.通过 cols 和 rows 属性来规定 textarea 的尺寸，更好的办法是使用 CSS 的height 和 width 属性

### `<table>`标签
表格

	tr(table row)元素定义表格行
	th(table head)元素定义表头
	td(table data)元素定义表格单元(数据)
	
### `<colgroup>`标签
表格，可单独设置每列的宽，同col一起使用（col表示列）

<img src="https://i.loli.net/2017/12/10/5a2d416f2959f.png">

----

### 常见空元素

在`HTML`元素中，没有内容的`HTML`元素被称为空元素。大多数`HTML`标签在开始标签`start tag`和结束标签`end tag`之间都具有内容，而某些标签则没有内容。`HTML`中，从开始标签到结束标签的所有代码，被称为`HTML`元素。

在`HTML`中，通常在一个空元素上使用一个闭标签是无效的。
	
	例如，<input type="text"> </input> 的闭标签是无效的 HTML。
	
常见的空元素有：

	<br> 换行
	<hr> 添加水平横线
	<img> 为网页插入图片，此元素有两个必需的属性：src 和 alt。通过在 <a> 
	      标签中嵌套 <img> 标签，给图像添加到另一个文档的链接。
	<input> 用于为基于Web的表单创建交互式控件，以便接受来自用户的数据。
	        此元素在 <form> 元素中使用，用来声明允许用户输入数据的 input 
	        控件。输入字段可通过多种方式改变，取决于 type 属性。
	<link> 指定了外部资源与当前文档的关系，最常见的用途是链接css文件。
	       此元素只能存在于 <head> 元素内部，不过它可出现任何次数。
	<meta> 描述 HTML 文档的元数据（元数据是数据的数据信息），<meta> 标签
	       通常位于 <head> 元素内部。

----
参考：[写代码啦] (https://xiedaimala.com/)





