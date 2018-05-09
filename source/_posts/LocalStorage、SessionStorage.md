---
title: LocalStorage、SessionStorage
date: 2018-03-03 16:27:31
categories: HTTP
tags:
---

#### `LocalStorage`

* `LocalStorage`是`Html5`提供的一个`API`。
* `LocalStorage`是浏览器上的`hash表`。

##### 常用`API`（`LocalStorage`和`SessionStorage`）

```
* localStorage.setItem(key, value) //保存数据
* localStorage.getItem(key) //读取数据
* localStorage.removeItem(key) //删除单个数据
* localStorage.clear() //删除所有数据
* localStorage.key(index) //得到某个索引的 key

//键值对通常以字符串存储，可以按自己的需要转换该格式。
```

##### `LocalStorage`特点

	1. LocalStorage 跟 HTTP 无关，HTTP 不会带上 LocalStorage 的值。
	2. 只有相同域名的页面才能互相读取 LocalStorage（没有同源那么严格）。
	3. 每个域名 LocalStorage 最大存储量为 5MB 左右（每个浏览器不一样）。
	4. 常用场景：记录有没有提示过用户（不敏感的信息，不能记录密码）。
	5. LocalStorage 永久有效，除非用户清理缓存。

举例1

    <script>
        //读取
        let a = localStorage.getItem('a')
        if(!a){
            a = 0
        }else{
            a = parseInt(a, 10) + 1
        }
        //存到本地
        localStorage.setItem('a', a)
    </script>


举例2

	<script>
        //读取
        let already = localStorage.getItem('已经提示了')
        if(!already){
            alert('你好，我们的网站改版了')
            localStorage.setItem('已经提示了', true)
        }
    </script>

##### `Cookie` 和 `LocalStorage`的区别？

	1. LocalStorage 跟 HTTP 无关，HTTP 不会带上 LocalStorage 的值。而 Cookie 属于 HTTP 的一部分，会被附加在每个 HTTP 请求中。
	2. 一般来说，LocalStorage 最大存储量为 5MB ，Cookie 最大存储量为 4MB 。 
	3. Cookie 默认在用户关闭页面后失效，但是后端可以强制设置有效期。LocalStorage 是永久有效，除非用户清理缓存。


---

#### `SessionStorage`

##### `SessionStorage` 和 `LocalStorage` 比较？

相同点

	* 都是用于客户端存储数据。
	* 存储数据的格式都是字符串形式。
	* 具有相同的 API 。

不同点

	* LocalStorage 永久有效，除非用户清理缓存。
	* SessionStorage 不是永久有效，当用户关闭浏览器窗口后，数据会被删除。
	* 相同浏览器的不同页面间可以共享相同的 LocalStorage （页面属于相同域名和端口），但不能共享 SessionStorage 的信息。
	
	//页面及标签页指顶级窗口，如果一个标签页包含多个 iframe 标签且他们属于同源页面，那么可以共享 SessionStorage 。

---
