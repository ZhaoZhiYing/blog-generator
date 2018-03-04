---
title: HTTP 缓存
date: 2018-03-03 19:53:51
categories: HTTP
tags:
---


#### `Cache-Control`

`Cache-Control`通用消息头被用于在 `HTTP` 请求和响应中通过指定指令来实现缓存机制。

**注意：**	首页不要设置缓存


##### 如何使`css` `js` 加载速度加快？

举例 `node.js`

	response.setHeader('Cache-Control', 'max-age=30') 
	// 表示当访问此网页后的 30s 内再次访问不会向服务器发起请求

##### 如何更新缓存？

1. 加版本号
2. 更改 `HTML` 的 `URL`，跟之前不一样即可，比如加个随机数。

---

#### `Expire`

##### `Expire` 和 `Cache-Control` 区别?

	* Expire 是指定了一个时间，在这个时间之后，HTTP 响应就过期。
	* Cache-Control 是指定一个时间范围，超过这个时间范围，HTTP 响应就过期。
	* Expire 是旧版缓存设置方法，Cache-Control 是新版缓存机制设置方法。

>如果还有一个设置了 "max-age" 或者 "s-max-age" 指令的 Cache-Control 响应头，那么 Expires 头就会被忽略。	

##### 为什么优先使用 `Cache-Control`?	

因为 `Expire` 指定的时间（日期/时间）指本地时间，如果用户的时间错乱，就会出问题。

---

#### `ETag`

##### 先了解下`MD5`

	* MD5 是一个摘要算法。将一个字符串，或文件，或压缩包，执行 MD5 后，就可以生成一个固定长度为128bit的串。如果有人修改过压缩包后，就会生成新的串。
	* MD5 的长度默认为 128bit，也就是128个0和1的二进制串。将二进制转成16进制，每4个bit表示一个16进制，所以128/4 = 32 换成16进制表示后，为32位。
	* MD5 最大的特点：如果内容的差异越小，算出的结果差异越大。

如下图

<img src="https://i.loli.net/2018/03/03/5a9ac12bcba07.png
">

##### `ETag`
	
	* 客户端发起请求一个文件时，这个文件的 MD5 被保存在 ETag 里。
	* 服务器处理请求，返回文件内容和头域（Header）(包括 Etag，例如"2e681a-6-5d044840")。
	* 客户端再次发起请求的时候，在头域（Header）中加入“If-match:Etag值”指令。
	* 服务器接受到请求后，通过发送过来的 If-Match 这个条件判断请求来验证资源是否修改。
	* 如果 If-Match === Etag值，则使用本地缓存。


##### `ETag` 和 `Cache-Control`区别

`Cache-Control`是直接不请求。`ETag`是请求但响应体是空的。

---



