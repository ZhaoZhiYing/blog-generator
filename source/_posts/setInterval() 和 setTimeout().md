---
title: setInterval() 和 setTimeout()
date: 2018-02-28 16:03:39
categories: JavaScript
tags:
---

#### `setInterval()`
重复调用一个函数或执行一个代码段，在每次调用之间具有固定的时间延迟。

* 使用 `clearInterval()` 方法来阻止函数的执行。由 `setInterval()` 返回的 `ID` 值用作 `clearInterval()` 方法的参数。

```
let n = 0;
let id = setInterval(()=>{ 
	n += 1
	console.log(n)
	if(n>=5){
		window.clearInterval(id)
	}
},3000)

// 1 2 3 4 5
```

---

#### `setTimeout()`
设置一个定时器，该定时器在定时器到期后执行一个函数或指定的一段代码，仅执行一次。

* 使用 `clearTimeout()` 方法来阻止函数的执行。由 `setTimeout()` 返回的 `ID` 值用作 `clearTimeout()` 方法的参数。

```
let n = 0;
let id = setTimeout(()=>{ 
	n += 1
	console.log(n)
},3000)

// 1
```

##### 所有的 `setInterval()`  都可以改写成 `setTimeout()`

```
let n = 0;
let id = setTimeout(function fn(){ 
	n += 1
	console.log(n)
	if(n<5){
		setTimeout(fn, 3000) //再次调用 fn
	}
},3000)

// 1 2 3 4 5
```

---

