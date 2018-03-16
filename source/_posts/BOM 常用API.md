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

	* Window.innerHeight //浏览器窗口的内部高度(包括滚动条)
	* Window.innerWidth // 浏览器窗口的内部宽度(包括滚动条)
	* Window.top //返回最顶层的父窗口。
	* Window.parent //返回父窗口。

方法
	
	//弹窗
	* alert(字符串) //显示带有一段消息和一个确认按钮的警告框。
	* prompt() //显示可提示用户输入的提示框。
	* confirm() //显示带有一段消息以及确认按钮和取消按钮的确认框。
	
	* window.print() //打印当前窗口的内容。
	* window.focus() //把键盘焦点给予一个窗口。
	* window.blur() //把键盘焦点从顶层窗口移开。 
	
	* window.open() //打开一个新的浏览器窗口或查找一个已命名的窗口。
	* window.close() //关闭浏览器窗口。
	* window.moveBy(x,y) //可相对窗口的当前坐标把它移动指定的像素。
	* window.moveTo(x,y) //把窗口的左上角移动到一个指定的坐标。
	* window.resizeBy(width,height) //按照指定的像素调整窗口的大小。
	* window.resizeTo(width,height) //把窗口的大小调整到指定的宽度和高度。
	
	* window.scrollBy(xnum,ynum) //按照指定的像素值来滚动内容。
	* window.scrollTo(xpos,ypos) //把内容滚动到指定的坐标。
	
	//计时事件
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

举例

	<div id="example"></div>
	<script>
	txt = "<p>浏览器代号: " + navigator.appCodeName + "</p>";
	txt+= "<p>浏览器名称: " + navigator.appName + "</p>";
	txt+= "<p>浏览器版本: " + navigator.appVersion + "</p>";
	txt+= "<p>启用Cookies: " + navigator.cookieEnabled + "</p>";
	txt+= "<p>硬件平台: " + navigator.platform + "</p>";
	txt+= "<p>用户代理: " + navigator.userAgent + "</p>";
	txt+= "<p>用户代理语言: " + navigator.systemLanguage + "</p>";
	document.getElementById("example").innerHTML=txt;
	</script> 

><div id="example"></div>
<script>
	txt = "<p>浏览器代号: " + navigator.appCodeName + "</p>";
	txt+= "<p>浏览器名称: " + navigator.appName + "</p>";
	txt+= "<p>浏览器版本: " + navigator.appVersion + "</p>";
	txt+= "<p>启用Cookies: " + navigator.cookieEnabled + "</p>";
	txt+= "<p>硬件平台: " + navigator.platform + "</p>";
	txt+= "<p>用户代理: " + navigator.userAgent + "</p>";
	txt+= "<p>用户代理语言: " + navigator.systemLanguage + "</p>";
	document.getElementById("example").innerHTML=txt;
</script> 

---
	
##### `Screen`对象

属性

	* screen.availHeight //可用的屏幕宽度（不包括 Windows 任务栏）
	* screen.availWidth //可用的屏幕高度（不包括 Windows 任务栏）
	* screen.height //返回屏幕的总高度
	* screen.width //返回屏幕的总宽度
	* screen.colorDepth //返回目标设备或缓冲器上的调色板的比特深度
	* screen.pixelDepth //返回屏幕的颜色分辨率（每象素的位数）

---	
	
##### `History`对象

属性

	* history.length //返回历史列表中的网址数

方法

	* history.back() //加载 history 列表中的前一个 URL
	* history.forward() //加载 history 列表中的下一个 URL
	* history.go() //加载 history 列表中的某个具体页面

---

##### `Location`对象

属性

	* location.hostname //返回 web 主机的域名
	* location.port //返回 web 主机的端口 （80 或 443）
	* location.protocol //返回所使用的 web 协议（http:// 或 https://）
	* location.pathname //返回当前页面的路径和文件名。
	
	* location.href //返回完整的 URL
	* location.hash //返回一个 URL 的锚部分
	* location.host //返回一个 URL 的主机名和端口
	* location.search //返回一个 URL 的查询部分

方法

	* assign() //载入一个新的文档
	* reload() //重新载入当前文档
	* replace() //用新的文档替换当前文档	

---	


