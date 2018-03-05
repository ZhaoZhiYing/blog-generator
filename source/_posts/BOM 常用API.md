---
title: BOM 常用API
date: 2018-02-23 21:54:46
categories: JavaScript
tags:
---

> `BOM`（`Browser Object Model`浏览器对象模型）提供与浏览器交互的方法和接口，可以访问和操作浏览器窗口。

`BOM`对象包括

	* Window对象 //表示浏览器中打开的窗口  
	* Navigator对象 //包含有关浏览器的信息  
	* Screen对象 //包含有关客户端显示屏幕的信息
	* History对象 //包含用户（在浏览器窗口中）访问过的 URL  
	* Location对象 //包含有关当前 URL 的信息

---

##### `Window`对象

属性

	* Window.history //对 History 对象的只读引用。请参数 History 对象。
	* Window.innerHeight //返回窗口的文档显示区的高度。
	* Window.innerWidth //返回窗口的文档显示区的宽度。
	* Window.self //返回对当前窗口的引用。等价于 Window 属性。
	* Window.top //返回最顶层的父窗口。
	* Window.parent //返回父窗口。

方法

	* alert(字符串) //显示带有一段消息和一个确认按钮的警告框。
	* prompt() //显示可提示用户输入的对话框。
	* confirm() //显示带有一段消息以及确认按钮和取消按钮的对话框。
	* open() //打开一个新的浏览器窗口或查找一个已命名的窗口。
	* close() //关闭浏览器窗口。
	* print() //打印当前窗口的内容。
	* focus() //把键盘焦点给予一个窗口。
	* blur() //把键盘焦点从顶层窗口移开。
	* moveBy() //可相对窗口的当前坐标把它移动指定的像素。
	* moveTo() //把窗口的左上角移动到一个指定的坐标。
	* resizeBy() //按照指定的像素调整窗口的大小。
	* resizeTo() //把窗口的大小调整到指定的宽度和高度。
	* scrollBy() //按照指定的像素值来滚动内容。
	* scrollTo() //把内容滚动到指定的坐标。
	* setInterval() //按照指定的周期（以毫秒计）来调用函数或计算表达式。
	* setTimeout() //在指定的毫秒数后调用函数或计算表达式。
	* clearInterval() //取消由 setInterval() 设置的 timeout。
	* clearTimeout() //取消由 setTimeout() 方法设置的 timeout。

---

##### `Navigator`对象

属性
	
	* appCodeName //返回浏览器的代码名
	* appName //返回浏览器的名称
	* appVersion //返回浏览器的平台和版本信息
	* cookieEnabled //返回指明浏览器中是否启用 cookie 的布尔值
	* platform //返回运行浏览器的操作系统平台
	* userAgent //返回由客户机发送服务器的 user-agent 头部的值

---
	
##### `Screen`对象

属性

	* availHeight //返回屏幕的高度（不包括Windows任务栏）
	* availWidth //返回屏幕的宽度（不包括Windows任务栏）
	* colorDepth //返回目标设备或缓冲器上的调色板的比特深度
	* height //返回屏幕的总高度
	* pixelDepth //返回屏幕的颜色分辨率（每象素的位数）
	* width //返回屏幕的总宽度	

---	
	
##### `History`对象

属性

	* length //返回历史列表中的网址数

方法

	* back() //加载 history 列表中的前一个 URL
	* forward() //加载 history 列表中的下一个 URL
	* go() //加载 history 列表中的某个具体页面

---

##### `Location`对象

属性

	* hash //返回一个URL的锚部分
	* host //返回一个URL的主机名和端口
	* hostname //返回URL的主机名
	* href //返回完整的URL
	* pathname //返回的URL路径名。
	* port //返回一个URL服务器使用的端口号
	* protocol //返回一个URL协议
	* search //返回一个URL的查询部分

方法

	* assign() //载入一个新的文档
	* reload() //重新载入当前文档
	* replace() //用新的文档替换当前文档	

---	


