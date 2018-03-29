---
title: Promise
date: 2018-01-30 22:26:59
categories: JavaScript
tags:
---

#### 「同步」和「异步」
`JavaScript` 语言本身并不慢，慢的是读写外部数据，比如等待 `AJAX` 请求返回结果。这个时候，如果对方服务器迟迟没有响应，或者网络不通畅，就会导致脚本的长时间停滞。为了解决这个问题，`Javascript` 语言将任务的执行模式分成两种：「同步」（`Synchronous`）和「异步」（`Asynchronous`）。

	* 一个任务分成两段，任务的第一段是向操作系统发出请求，要求读取文件。任务的第二段是处理文件。
	* 「同步」是指后一个任务等待前一个任务执行结束，然后再执行。

```
console.log('A')
!function(){
  console.log('B')
}.call()
console.log('C')

//A B C
```

	*「异步」是指前一个任务先发送一个请求，不等待返回（就是第二段的处理文件），直接进行下一个任务。

```
console.log('A')
setTimeout(function(){
  console.log('B')
},1000)
console.log('C')

//A C B
// console.log('C') 就是异步执行的
```

---

#### 回调函数
* 一个函数被作为参数传给另一个函数去调用，这样的函数就是回调函数。
* 换言之，回调函数，就是把任务的第二段单独写在一个函数里面，在特定的事件或条件发生时，调用这个函数。

* 同步回调。

```
//定义一个函数 add
function add(a, b, callback) {
    callback(a+b)
}

add(1,2,function(result) {
    console.log("result:" + result)
})

add(1,2,function(result){
    console.log("结果是:" + result)
})

//result:3 
//结果是:3 
```
* 异步回调。经常使用以下方法：
	* 对于异步执行（例如读取文件和发出`HTTP`请求）
	* 在事件监听器/处理程序中
	* 在`setTimeout`和`setInterval`方法中

```
function f2(){
    console.log('bar第二') 
}
function f1(callback){
    setTimeout(function(){
        console.log('foo第一')
        callback()
    },1000)
}

f1(f2) 
//foo第一 bar第二 
```

但是，一旦嵌套层级多了，就会形成回调地狱，代码结构就容易变得很不直观。如下：


	setTimeout(function(){
	  left(function(){
	    setTimeout(function(){
	       left(function(){
	         setTimeout(function(){
	           left();
	         },2000);
	       });
	    }, 2000);
	  });
	}, 2000);


---

#### `Promise`（全局 `window` 的属性）
##### `Promise` 对象有以下两个特点:
1.对象的状态不受外界影响。`Promise `对象代表一个异步操作，有三种状态：

	pending: 初始状态，既不是成功，也不是失败状态。
	fulfilled: 意味着操作成功完成。
	rejected: 意味着操作失败。
	
	//只有异步操作的结果，可以决定当前是哪一种状态。
	//任何其他操作都无法改变这个状态。

2.一旦状态改变，就不会再变，任何时候都可以得到这个结果。

`Promise` 的状态的变化途径只有两种：

	1.异步操作从 pending 到 fulfilled ，表示异步操作成功，Promise 对象传回一个值，状态变为 resolved。
	2.异步操作从 pending 到 rejected ，表示异步操作失败，Promise 对象抛出一个错误，状态变为 rejected。
	
	//只要这两种情况发生，状态就凝固不会再变了，会一直保持这个结果。
	//就算改变已经发生了，你再对 Promise 对象添加回调函数，也会立即得到这个结果。
	//这与事件完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

	
##### 基本用法
语法

	new Promise(function(resolve, reject) /* executor */ )

	// executor 是 resolve 和 reject 两个函数。由 JavaScript 引擎提供。
	// resolve 函数，在异步操作成功时调用，并将异步操作的结果，作为参数传递出去。
	// reject 函数，在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

举例

	let promise = new Promise(function(resolve, reject) {
	  // ... some code
	  if (/* 异步操作成功 */){
	     resolve(value);
	  } else {
	     reject(error);
	  }
	});



##### `then`

	// then 方法可以接受两个回调函数作为参数。
	//第一个回调函数是 Promise 对象的状态变为 resolved 时调用。
	//第二个回调函数是 Promise 对象的状态变为 rejected 时调用。

举例

	let promise = new Promise(function(resolve, reject) {
	   // ... some code
	}).then(function(value) {
	   // success
	}, function(error) {
	   // failure
	});


##### `catch`
	
	// catch 是用于指定发生错误时的回调函数。效果和写在 then 的第二个参数里面一样。
	//建议总是使用 catch，catch() 使回调报错时不会卡死 JS 而是会继续往下执行。
	// Promise 对象的错误具有"冒泡"性质，会一直向后传递，直到被捕获为止。也就是说，错误总是会被下一个 catch 语句捕获。

举例

	let promise = new Promise(function(resolve, reject) {
	   // ... some code
	}).then(function(value) {
	   // success
	}).catch(function(error) {
		// failure
	})
  
---
