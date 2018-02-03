---
title: Promise
date: 2018-01-30 22:26:59
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

* 「异步」是指前一个任务先发送一个请求，不等待返回（就是第二段的处理文件），直接进行下一个任务。

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
function add(a, b, callback) {
    callback(a+b)
}

add(1,2,function(result) {
    console.log("result:" + result)
})

add(1,2,function(result){
    console.log("结果是:" + result)
})

//result:3 结果是:3 
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


	step1(function (value1) {
	  step2(value1, function(value2) {
	    step3(value2, function(value3) {
	      step4(value3, function(value4) {
	        // ...
	      })
	    })
	  })
	})


---

#### `Promise`对象
* 回调函数本身并没有问题，它的问题出现在多个回调函数嵌套。而`Promise`对象可以使异步操作具备同步操作的接口，使程序具备正常的同步运行的流程，避免了嵌套多个层级。

比如，异步操作`f1`返回一个`Promise`对象，它的回调函数`f2`写法如下。

	(new Promise(f1)).then(f2);
	
这种写法对于多层嵌套的回调函数尤其方便。

	(new Promise(step1))
	  .then(step2)
	  .then(step3)
	  .then(step4);	
	  
`Promise`的最大问题是代码冗余，原来的任务被`Promise`包装了一下，不管什么操作，一眼看去都是一堆`then`，原来的语义变得很不清楚。  

##### 基本用法
语法

```
new Promise(function(resolve, reject) /* executor */ )
```

##### `executor`

```
// executor 是带有 resolve 和 reject 两个参数的函数。
// Promise 构造函数执行时立即调用 executor 函数。
// resolve 和 reject 两个函数作为参数传递给 executor（ executor 函数在 Promise 构造函数返回新建对象前被调用）。
```

##### `resolve` `reject`
```
// resolve 函数，在异步操作成功时调用，并将异步操作的结果，作为参数传递出去
// reject 函数，在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。
```

##### `then`
```
// then 方法可以接受两个回调函数作为参数。
//第一个回调函数是 Promise 对象的状态变为 resolved 时调用。
//第二个回调函数是 Promise 对象的状态变为 rejected 时调用。
```
	  
---

参考：

[阮一峰-Promise对象](http://javascript.ruanyifeng.com/advanced/promise.html#toc0)  

[写代码啦](https://xiedaimala.com/)