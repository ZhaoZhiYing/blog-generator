---
title: stopPropagation() 和 preventDefault()
date: 2018-02-21 18:03:41
categories: JavaScript
tags:
---

#### `stopPropagation()`	
在整个事件流的任何位置（捕获或冒泡）都可以通过调用事件的`stopPropagation()`方法停止事件的传播过程。	

举例

```
grand1.addEventListener('click', function fn1(e){
  console.log('爷爷')
  e.stopPropagation()//事件不再被分派到其他节点
},true)
parent1.addEventListener('click', function fn2(){
  console.log('爸爸')
},false)
child1.addEventListener('click', function fn3(){
  console.log('儿子')
})
//当点击‘儿子’时，打印：爷爷
```

#### `preventDefault()`
阻止元素的默认事件。例如：

* 当点击提交按钮时阻止对表单的提交
* 当点击 `a` 链接时页面不会跳转

```
<a href="https://www.google.com.hk/?hl=zh-cn">谷歌</a>  

<script>
	$("a").click(function(event){             
		event.preventDefault() //页面不会跳转  
	})
</script>	
```

---