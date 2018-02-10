---
title: Cookie
date: 2018-02-05 09:29:27
tags:
---

##### `Cookie`是什么？

`Cookie` 是浏览器在你访问网页时，存储在你电脑上的一小段文本。

---

##### `Cookie` 特点

1.服务器通过 `Set-Cookie` 响应头设置 `Cookie`。

```
	Set-Cookie: key=value;
	//等号两边不能有空格
```

2.浏览器得到 `Cookie` 之后， 每次请求都要带上 `Cookie`。

3.服务器读取 `Cookie` 就知道登录用户的信息。

---

##### `Cookie` 有效期
 默认有效期20分钟左右，不同浏览器策略不同。后端可以强制设置有效期。

---

##### 同源策略

`Cookie`同源策略跟 `AJAX` 的同源策略稍微有些不同。
当请求 `qq.com` 下的资源时，浏览器会默认带上 `qq.com` 对应的 `Cookie`，不会带上 `baidu.com` 对应的 `Cookie`。当请求 `v.qq.com` 下的资源时，浏览器不仅会带上 `v.qq.com` 的 `Cookie`，还会带上 `qq.com` 的 `Cookie`。
另外 `Cookie` 还可以根据路径做限制。

---

##### `Cookie`缺点

1.`Cookie`会被附加在每个`HTTP`请求中，所以无形中增加了流量。

2.由于在`HTTP`请求中的`Cookie`是明文传递的，所以安全性成问题，除非用`HTTPS`。

3.`Cookie`的大小限制在4KB左右，对于复杂的存储需求来说是不够用的。

---

