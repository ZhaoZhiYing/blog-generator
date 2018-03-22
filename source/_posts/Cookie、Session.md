---
title: Cookie、Session
date: 2018-02-05 09:29:27
categories: HTTP
tags:
---
#### `Cookie`

##### `Cookie`是什么？

**注意：**前端永远不要读写 `Cookie`，交给后端。

`Cookie` 是浏览器在你访问网页时，存储在你电脑上的一小段文本。后面再访问网页时，都必须带上这段文本。

##### `Cookie`的特点
 
	1. 服务器通过 Set-Cookie 响应头设置 Cookie ，给客户端一串字符串。
	2. 客户端得到 Cookie 之后， 每次访问相同域名的网页时，都要带上 Cookie 。
	3. 服务器读取 Cookie 就知道登录用户的信息。客户端要在一段时间内保存这个 Cookie 。
	4. Cookie 默认在用户关闭页面后失效，但是后端可以强制设置有效期。

举例`server.js`

	response.setHeader('Set-Cookie',`sign_in_email=${email}`)
	
	
##### 同源策略

	* Cookie 同源策略跟 AJAX 的同源策略稍微有些不同。
	* 浏览器的同源政策规定，两个网址只要域名相同和端口相同，就可以共享  Cookie 。
	* 注意，这里不要求协议相同。也就是说， http://example.com 设置的 Cookie ，可以被 https://example.com 读取。

##### `Cookie`的缺点

	1. Cookie 会被附加在每个 HTTP 请求中，所以无形中增加了流量。
	2. 由于在 HTTP 请求中的 Cookie 是明文传递的，所以安全性成问题，用户能够篡改密码，除非用 HTTPS 。
	3. Cookie 的大小限制在 4KB 左右，对于复杂的存储需求来说是不够用的。

---

#### `Session`

##### `Session`是什么？

`Session` 是在无状态的 `HTTP` 协议下，服务端记录用户状态时用于标识具体用户的机制。

* `Session`解决了`Cookie`的安全性问题。
* `Session`是服务器上的`hash表`。


##### `Session`的用法

```
1. 服务器通过 cookie 给用户一个 sessionId (随机数)。
2. 服务器有一块内存（哈希表）保存了所有的 session 。 
3. 每次用户访问服务器的时候，服务器通过 sessionId 去读取对应的 session，得到用户的隐私信息，比如 id email 。
```

举例`server.js`

```
//Session
let sessionId = Math.random() * 100000 
sessions[sessionId] = {sign_in_email: email}

//Set-Cookie
response.setHeader('Set-Cookie',`sessionId = ${sessionId}`)
```

#### 不基于 `Cookie` 的 `Session`

`Session` 还可以通过 `LocalStorage` + 查询参数 来存储 `sessionId`。

---

#### 问题归纳

##### 1.`Cookie`如何设置过期时间？

	cookie.setMaxAge(0);//不记录cookie
	
	cookie.setMaxAge(-1);//会话级cookie，关闭浏览器失效
	
	cookie.setMaxAge(60*60);//过期时间为1小时
	

##### 2.如何删除 `Cookie`？

设置 `Expires` 参数为以前的时间即可。

	document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT";


##### 3.`Cookie` 和 `Session` 的关系以及区别？

关系

	Session 通常是基于 Cookie 实现，其 SessionId 是通过 Cookie 发送给客户端的。

区别

	1. Cookie 数据保存在客户端。Session 数据保存在服务器端。
	2. 由于在 HTTP 请求中的 Cookie 是明文传递的，所以安全性成问题，用户能够篡改密码。所以一般情况，登录信息等重要信息存储在 Session 中，其他信息存储在 Cookie 中。 

---	