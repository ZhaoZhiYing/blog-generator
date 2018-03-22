---
title: JSONP
date: 2018-01-25 10:18:42
categories: HTTP
tags:
---

#### 数据库是什么？
只要能长久地存数据，就是数据库

1. 文件系统是一种数据库
2. `MySQL` 是一种数据库

---

#### 同源策略
它是在1995年，由`Netscape`提出的一个著名的安全策略，现在所有支持 `JavaScript` 的浏览器都会使用这个策略。

所谓"同源"指的是"三个相同"：

* 协议相同
* 域名相同
* 端口相同

如果非同源，共有三种行为受到限制。

* `Cookie` `LocalStorage` 和 `IndexDB` 无法读取。
* `DOM` 无法获得。
* `AJAX` 请求不能发送。

同源政策规定，`AJAX`请求只能发给同源的网址，否则就报错。有三种方法规避这个限制。

* `JSONP`
* `WebSocket`
* `CORS`

这里，我们主要讲 `JSONP`。

---

#### 局部刷新怎么做？
有没有想过，不返回`HTML`，返回`JS`

```
//方案一：用 image 造 get 请求
button.addEventListener('click', (e)=>{
    let image = document.createElement('img')
    image.src = '/pay'
    image.onload = function(){ // 状态码是 200~299 则表示成功
        alert('成功')
    }
    image.onload = function(){ // 状态码大于等于 400 则表示失败
        alert('失败')
    }
})
```
```
//方案二：用 script 造 get 请求
button.addEventListener('click', (e)=>{
    let script = document.createElement('script')
    script.src = '/pay'
    document.body.appendChild(script)
    script.onload = function(e){ // 状态码是 200~299 则表示成功
        e.currentTarget.remove()
    }
    script.onload = function(e){ // 状态码大于等于 400 则表示失败
        e.currentTarget.remove()
    }
})
```
```
//后端代码
...
if (path === '/pay'){
    let amount = fs.readFileSync('./db', 'utf8')
    amount -= 1
    fs.writeFileSync('./db', amount)
    response.setHeader('Content-Type', 'application/javascript')
    response.write('amount.innerText = ' + amount)
    response.end()
}
...
```
无刷新，局部更新页面内容，这种技术叫做`SRJ` - `Server Rendered JavaScript`

---

#### `JSONP`


##### 什么是 `JSONP`?
* `JSONP`是`JSON with Padding`的简称。
* `JSONP` 是服务器与客户端跨源通信的常用方法。是指动态创建 `script`，并调用我给你的`callback`技术。详细过程如下：

```
* 请求方：frank.com 的前端程序员（浏览器）
* 响应方：jack.com 的后端程序员（服务器）

1. 请求方创建 script，src 指向响应方，同时传一个查询参数 ?callbackName=xxx ，xxx 是随机数。
2. 响应方根据查询参数 callbackName ，构造形式如 xxx.call(undefined, '你要的数据') 这样的响应。
3. 浏览器接收到响应，就会执行 xxx.call(undefined, '你要的数据')。 
4. 那么请求方就知道了他要的数据。 

```

约定

* `callbackName` 约定叫做 `callback` 
* `xxx` 是随机数，比如：`'frank'+ parseInt(Math.random() * 100000,10)`

```
//方案三：JSONP
button.addEventListener('click', (e)=>{
    let script = document.createElement('script')
    let functionName = 'frank'+ parseInt(Math.random()*10000000 ,10)
    window[functionName] = function(){  // 每次请求之前搞出一个随机的函数
        amount.innerText = amount.innerText - 0 - 1
    }
    script.src = '/pay?callback=' + functionName
    document.body.appendChild(script)
    script.onload = function(e){ // 状态码是 200~299 则表示成功
        e.currentTarget.remove()
        delete window[functionName] // 请求完了就干掉这个随机函数
    }
    script.onload = function(e){ // 状态码大于等于 400 则表示失败
        e.currentTarget.remove()
        delete window[functionName] // 请求完了就干掉这个随机函数
    }
})

 //上面代码用 jQuery 写
 $.ajax({
 url: "http://jack.com:8002/pay",
 dataType: "jsonp",
	 success: function( response ) {
	     if(response === 'success'){
	    	 amount.innerText = amount.innerText - 1
	     }
	 }
 })
 $.jsonp()
```

```
//后端代码
...
if (path === '/pay'){
    let amount = fs.readFileSync('./db', 'utf8')
    amount -= 1
    fs.writeFileSync('./db', amount)
    let callbackName = query.callback
    response.setHeader('Content-Type', 'application/javascript')
    response.write(`
        ${callbackName}.call(undefined, 'success')
    `)
    response.end()
}
...
```

##### `JSONP` 为什么不支持 `POST` 请求？

`JSONP`是通过动态创建 `script` 实现的，`script`标签的`src`属性没有跨域的限制。如果用`post`，就会检查是否跨域。

---

