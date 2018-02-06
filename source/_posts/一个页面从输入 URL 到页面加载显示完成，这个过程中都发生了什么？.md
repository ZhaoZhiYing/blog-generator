---
title: 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？
date: 2017-10-19 13:42:12
tags:
---


### 1.`DNS`解析

* `DNS`全称：域名解析系统`Domain Name System`。
* `DNS`解析是指根据域名查找`IP`地址。 

##### 概念解释：

* `IP`地址：是`IP`协议提供的一种统一的地址格式，它为互联网上的每一个网络和每一台主机分配一个逻辑地址。
* 域名：相当于`IP`地址的面具，域名的作用的便于人类使用。例如，`www.wikipedia.org`是一个域名，对应的`IP`地址是`208.80.152.2`。

##### 解析过程

以`www.google.com`为例

1. 本地域名服务器首先检查自身缓存，如果存在记录则直接返回结果。
2. 如果记录老化或不存在
	* 本地域名服务器会向根域名服务器发送查询报文`query www.google.com`。
	* 如果根域名服务器也不存在该域名，本地域名服务器会向`.com`顶级域名服务器发送查询报文`query www.google.com`。
	* 如果`.com`顶级域名服务器也不存在该域名，本地域名服务器会向`.google.com`顶级域名服务器发送查询报文`query www.google.com`。得到主机`www`的记录，存入自身缓存并返回给客户端。

---

#### 知识展开

#### `URL`
统一资源定位符，通俗地称为`Web`地址。`URL`通常由以下几部分组成：

	* 协议：由一串不区分大小写的字母组成，以 : 作为结束符。常用的有http、https等。
	* 身份验证：可选，一般的协议(`http\https`等)都会使用默认的匿名形式进行数据获取（格式：`username:password@hostname`）。
	* 域名：服务器(计算机)域名系统 (DNS) 主机名或 IP 地址。
	* 端口号：可选，通过冒号与主机名分开，省略时使用默认端口号。各种传输协议都有默认的端口号，`http`的默认端口为`80`。
	* 路径：由零或多个“/”符号隔开的字符串，一般用来表示主机上的一个目录或文件地址。
	* 查询参数：可选，可有多个参数，用“&”符号隔开，每个参数的名和值用“=”符号隔开。
	* 锚点：例如一个网页中有多个名词解释，可使用锚点直接定位到某一名词解释。

如图

<img src='https://i.loli.net/2018/02/05/5a7836443733e.png
'>

##### 域名级别

	www.google.com 是三级域名
	google.com 是二级域名（正常经常忽略.com，baidu.com 称为一级域名）
	.com 是一级域名（顶级域名）
	www.baidu.com 和 baidu.com 不是同一个域名，只是共有一个二级域名。

---
    
#### 2.`TCP`连接

浏览器根据 `IP` 地址向服务器发起 `TCP` 连接，与浏览器建立 `TCP` 三次握手：

	1. 主机向服务器发送一个建立连接的请求（你好，认识一下咯）。
	2. 服务器接到请求后发送同意连接的信号（好的，很高兴认识你）。
	3. 主机接到同意连接的信号后，再次向服务器发送了确认信号（嘿嘿，我也很高兴认识你），自此，主机与服务器两者建立了连接。

---

#### 知识展开

* 通常使用的网络是在`TCP/IP`协议族的基础上运作的。而`HTTP`属于它内部的一个子集。
* `TCP/IP`协议族一共分为4层：应用层、传输层、网络层和数据链路层。

```
应用层：决定了向用户提供应用服务时通信的活动。包括 FTP(文件传输协议)、DNS(域名解析系统)、HTTP协议。

传输层：传输层对上层应用层，提供处于网络连接中的两台计算机之间的数据传输。包括 TCP(传输控制协议)、UDP(用户数据报协议)。

网络层：处理在网络上流动的数据包（数据包是网络传输的最小数据单位）。该层规定了通过怎样的路径到大对方计算机，并把数据包传送给对方。

数据链路层：处理连接网络的硬件部分。比如硬件的设备驱动、光纤等物理可见部分。
```

---

#### 3.发送`HTTP`请求

`HTTP`请求报文是由三部分组成：请求行, 请求报头和请求正文。

---

#### 4.服务器处理请求并返回`HTTP`报文

`HTTP`响应报文也是由三部分组成：状态码, 响应报头和响应报文。

---

#### 知识展开

##### `HTTP`协议的作用指导服务器和浏览器如何沟通。

	* 浏览器负责发起请求
	* 服务器在 80 端口接收请求
	* 服务器负责返回内容（响应）
	* 浏览器负责下载响应内容

##### `Https`和`Http`的区别

	Https 加密  
	Http 有安全隐患，造成密码被盗

##### 用`curl`发请求
	
	curl -s -v -H "Frank: xxx" -- "https://www.baidu.com"
		
	curl -X POST -d "username=ff&password=123" -s -v  -- "http://localhost:8080/path"
		
	-X	curl 默认的 HTTP 动词是 GET，使用 -X 参数可以支持其他动词。
	-s 不显示进度条
	-v 显示请求和响应
	-H 添加响应头
	-d 要下载的内容
	
##### 请求格式

	1 动词 路径 协议/版本
	(POST / HTTP/1.1 或 GET / HTTP/1.1)
	2 Key1: value1
	2 Key2: value2
	2 Key3: value3
	2 Content-Type: application/x-www-form-urlencoded //上传格式，默认为text/html
	2 Host: www.baidu.com //根域名
	2 User-Agent: curl/7.54.0  //代理
	3 永远是回车（为了区分第二部分和第四部分）
	4 要上传的数据（可以是空的）
	
动词

	Get 获取信息
	post 上传信息
	put 更新
	patch 局部更新
	delete 删除
	
注意事项

	1. 请求最多包含四部分，最少包含三部分。（也就是说第四部分可以为空）
	2. 第三部分永远都是一个回车（\n）
	3. 动词有 GET POST PUT PATCH DELETE HEAD OPTIONS 等
	4. 这里的路径包括「查询参数」，但不包括「锚点」
	5. 如果你没有写路径，那么路径默认为 /
	6. 第 2 部分中的 Content-Type 标注了第 4 部分的格式


##### 响应格式

	1 协议/版本号 状态码 状态解释
	2 Key1: value1
	2 Key2: value2
	2 Content-Length: 17931
	2 Content-Type: text/html
	3
	4 要下载的内容

##### 状态码

	1xx 不常用
	2xx 表示成功   200响应成功   204创建成功
	3xx 表示滚吧（重定向）301永久搬走   302临时外出 
	4xx 表示你丫错了（客户端错误）
	5xx 表示好吧，我错了（服务器错误）


##### `Content-Type`

下面是几个常见的`Content-Type`

	* text/html
	* text/plain
	* text/css
	* text/javascript
	* application/x-www-form-urlencoded
	* multipart/form-data
	* application/json
	* application/xml 
	

##### `GET` 
		

	//GET 请求
	1 GET / HTTP/1.1
	2 Host: baidu.com
	2 Accpet: text/html
	
	//GET 响应
	1 HTTP/1.1 200 OK
	2 Content-Type: text/html; charset=utf-8
	2 Content-Length: 10000
	

##### `POST`

	//POST 请求
	1 POST /path HTTP/1.1
	2 Host: localhost:8080
	2 User-Agent: curl/7.54.0
	2 Accept: */*
	2 Content-Length: 24
	2 Content-Type: application/x-www-form-urlencoded
	3 
	4 username=ff&password=123
	
	//POST 响应
	1 HTTP/1.1 200 OK
	2 Content-Type: application/json
	2 Content-Length: 20
	3 
	4 

--- 
 
#### 浏览器解析渲染页面

浏览器是一个边解析边渲染的过程。首先浏览器解析`HTML`文件构建`DOM`树，然后解析`CSS`文件构建渲染树，等到渲染树构建完成后，浏览器开始布局渲染树并将其绘制到屏幕上。

---
   
#### 6.关闭`TCP`连接或继续保持连接

通过四次挥手关闭连接。一端断开连接需要两次挥手（请求和回应），两端断开连接就需要四次挥手。

---

