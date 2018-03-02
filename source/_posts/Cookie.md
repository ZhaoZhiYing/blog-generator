---
title: Cookie
date: 2018-02-05 09:29:27
categories: HTTP
tags:
---

##### `Cookie`是什么？

`Cookie` 是浏览器在你访问网页时，存储在你电脑上的一小段文本。后面再访问网页时，都必须带上这段文本。


##### `Cookie` 特点

1.服务器通过 `Set-Cookie` 响应头设置 `Cookie`。

	Set-Cookie: key=value;
	//等号两边不能有空格

2.浏览器得到 `Cookie` 之后， 每次请求都要带上 `Cookie`。

3.服务器读取 `Cookie` 就知道登录用户的信息。

##### 同源策略

`Cookie`同源策略跟 `AJAX` 的同源策略稍微有些不同。

浏览器的同源政策规定，两个网址只要域名相同和端口相同，就可以共享 `Cookie`。

注意，这里不要求协议相同。也就是说，`http://example.com` 设置的`Cookie`，可以被 `https://example.com` 读取。

##### `Cookie`缺点

1.`Cookie`会被附加在每个`HTTP`请求中，所以无形中增加了流量。

2.由于在`HTTP`请求中的`Cookie`是明文传递的，所以安全性成问题，除非用`HTTPS`。

3.`Cookie`的大小限制在4KB左右，对于复杂的存储需求来说是不够用的。

---

