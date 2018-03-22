---
title:  HTML 标签
date: 2017-10-24 10:32:19
categories: HTML
tags:
---


在 `CSS` 中，`HTML` 中的标签元素大概被分为三种类型：

	* 块级元素
	* 内联元素
	* 内联块级元素

常用的块状元素

	* <div> //定义一个分隔区块或者一个区域部分。
	* <p> //定义一个段落。
	* <h1>…<h6> //定义标题。
	* <ol> //定义一个有序列表。
	* <ul> //定义一个无序列表
	* <dl> //定义一个描述列表。
		//与 <dt> 和 <dd> 一起使用。
		//<dt>（定义项目/名字）
		//<dd>（描述每一个项目/名字）
	* <table> //创建一个表格。
	* <address> //定义文档作者/所有者的联系信息。
	* <blockquote> //定义摘自另一个源的块引用。
	* <form> //创建供用户输入的表单。

常用的内联元素

	* <a> //定义超链接，用于从一个页面链接到另一个页面。
	* <span> //提供了一种将文本的一部分或者文档的一部分独立出来的方式。
	* <br> //换行符。
	* <i> //斜体。
	* <em> //用来呈现为被强调的文本。
	* <strong> //用来定义计算机程序的样本重要的文本。
	* <label> //为 input 元素定义标注（标记）。
	* <q> //定义一个短的引用。浏览器经常会在这种引用的周围插入引号。
	* <var> //定义变量。可以将此标签与 <pre> 及 <code> 标签配合使用。
	* <cite> //定义作品（比如书籍、歌曲、电影、电视节目、绘画、雕塑等等）的标题。
	* <code> //定义计算机代码文本。

常用的内联块级元素

	* <img> //
	* <input> //


---

### 标签详解

#### `<iframe>`

在当前页面嵌套一个页面。

	* 默认宽 100px 高 50px
	* 默认有难看的 border，可在 CSS 中设置。

属性
	
	* height //规定 <iframe> 的高度。
	* width //规定 <iframe> 的宽度。
	* name //规定 <iframe> 的名称。
		//需结合 a 标签使用，否则无意义
	* src 指定路径
		绝对 URL - 指向另一个网站（比如 src="http://www.example.com/default.htm"）
		相对 URL - 指向网站中的一个文件（比如 src="default.htm"）
	
	// HTML5 中的新属性
	* srcdoc //规定页面中的 HTML 内容显示在 <iframe> 中。
	* seamless //规定 <iframe> 看起来像是父文档中的一部分。
	* sandbox //对 <iframe> 的内容定义一系列额外的限制。
		"" //启用所有限制条件
		allow-same-origin //允许将内容作为普通来源对待。如果未使用该关键字，嵌入的内容将被视为一个独立的源。
		allow-top-navigation //嵌入的页面的上下文可以导航（加载）内容到顶级的浏览上下文环境。如果未使用该关键字，这个操作将不可用。
		allow-forms //允许表单提交。
		allow-scripts //允许脚本执行。

示例一：`name`

因为 `a` 链接的 `target` 属性匹配了 `ifrme` 的 `name` 属性，所以链接点击后将显示在 `iframe` 中。

<img src="https://i.loli.net/2018/03/16/5aab6bff06e60.png
">

示例三：`src` `width` `height`

<img src="https://i.loli.net/2018/03/16/5aab6b621ca04.png
">

示例二：`srcdoc`

<img src="https://i.loli.net/2018/03/16/5aab6bdd59442.png
">
	
	
#### `<a>`

属性

	* target //该属性指定在何处显示链接的资源。
		_self //默认属性。当前页面加载。
		_blank //新窗口打开
		_parent //父级页面打开。如果没有，同_self。
		_top //顶级页面加载。如果没有，同_self。 
	* href //规定链接的目标地址。
		href="//qq.com" //无协议地址
		href="#xxx" //锚点#，不发起请求
		href="?name=qq" //发起请求
		href="./xxx.html" //相对路径 
		href="javascript:;" //让 a 标签不跳转
		href="javascript:alert(1)" //执行一段代码
		href="http://write.blog.csdn.net" //绝对 URL，指向另一个站点
		a href="" //刷新页面
		href="#top" //返回到页面顶部
		href="#" //返回到页面顶部
		

	// HTML5 中的新属性
	* download //指示浏览器下载 URL 而不是导航到 URL
	* type //规定目标 URL 的 MIME 类型。仅在 href 属性存在时使用。
		注：MIME 是指示文件的类型（描述的内容格式，例如声音文件可能会被标记  audio/ogg，或图像文件 image/png）
	* media //规定目标 URL 的媒介类型。默认值：all。仅在 href 属性存在时使用。
	...

如何实现浏览器以下载形式接收请求，而不是显示页面？

	// a 标签里加 download
	<a href="/images/logo.png" download="logo">
	
	// HTTP 请求
	Content-type: application/octet-stream

---

#### 常见空元素

在`HTML`元素中，没有内容的`HTML`元素被称为空元素。大多数`HTML`标签在开始标签`start tag`和结束标签`end tag`之间都具有内容，而某些标签则没有内容。`HTML`中，从开始标签到结束标签的所有代码，被称为`HTML`元素。

在`HTML`中，通常在一个空元素上使用一个闭标签是无效的。
	
	例如，<input type="text"> </input> 的闭标签是无效的 HTML。
	
常见的空元素有：

	* <br> //换行符。
	* <hr> //添加水平横线。
	* <img> //定义超链接，用于从一个页面链接到另一个页面。
	* <input> //在 <form> 元素中使用，用来声明允许用户输入数据的 input 控件。
	* <link> //定义文档与外部资源的关系。最常见的用途是链接 css 文件。
	* <meta> //描述 HTML 文档的元数据（元数据是数据的数据信息），<meta> 标签通常位于 <head> 元素内部。

---






