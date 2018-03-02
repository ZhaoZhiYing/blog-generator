---
title: 实现一个 jQuery 的 API
date: 2018-01-01 16:44:38
categories: JavaScript
tags:
---
#### `getSiblings`获取一个节点的所有兄弟节点
	<ul>
	  <li id="item1">选项1</li>
	  <li id="item2">选项2</li>
	  <li id="item3">选项3</li>
	  <li id="item4">选项4</li>
	  <li id="item5">选项5</li>
	</ul>

定义一个伪数组 `array`，然后遍历伪数组，将`!== item3`的节点放进这个伪数组，最后得到这个节点的所有兄弟节点。

	var allChildren = item3.parentNode.children 
	var array = { 
		length:0
	}
	for(let i = 0; i<allChildren.length; i++){
		if (allChildren[i] !== item3){
			array[array.length] = allChildren[i]
			array.length += 1
		}
	}
	
封装成函数

	function getSiblings(node){
		var allChildren = node.parentNode.children 
		var array = { 
			length:0
		}
		for(let i = 0; i<allChildren.length; i++){
			if (allChildren[i] !== node){
				array[array.length] = allChildren[i]
				array.length += 1
			}
		}
		return array
	}
	getSiblings(item3)//调用
		

#### `addClass`为元素添加指定的样式类名

	item3.classList.add('a')
	item3.classList.add('b')
	item3.classList.add('c')
	
上面代码优化后如下（这里用到了箭头函数）

	var classes = {'a':true, 'b':true, 'c':false,}
	classes.forEach((value) => item3.classList.add(value))
	
加上`remove`

	var classes = {'a':true, 'b':true, 'c':false,}
	for(let key in classes){
		var value = classes[key]
		if(value){
			item3.classList.add(key)
		}else{
			item3.classList.remove(key)
		}
	}
	
封装成函数

	function addClass(node,classes){
		for(let key in classes){
			var value = classes[key]
			if(value){
				node.classList.add(key)
			}else{
				node.classList.remove(key)
			}
		}	
	}	
	addClass(item3,{'a':true, 'b':true, 'c':false,})//调用
	
优化代码（这里用到了三元运算符）

	function addClass(node,classes){
	  for(let key in classes){
	      var value = classes[key]
	      var methodName = value ? 'add' : 'remove'
	      node.classList[methodName](key)
	    }	
	}	
	addClass(item3,{'a':true,'b':true,'c':false,})//调用
	
上面代码等于下面

	function addClass(node,classes){
		classes.forEach((value) => node.classList.add(value))
	}	
	addClass(item3,['a','b','c'])//调用
		
上面两个 API 的弊端：如果有人已经定义过getSiblings ，会被这次覆盖。而且不方便调用。运用 **命名空间** 能解决这个问题。

	window.zzdom = {} //声明变量名 zzdom
	zzdom.getSiblings = getSiblings 
	zzdom.addClass = addClass
	//调用
	zzdom.getSiblings.call(item3)  
	zzdom.addClass.call(items, {a:true, b:false, c:true})	
代码更新如下

	window.zzdom = {}		
	zzdom.getSiblings = function (node){ 
	var allChildren = node.parentNode.children 
	var array = { 
	    length:0
	}
	for(let i = 0; i<allChildren.length; i++){
	    if (allChildren[i] !== node){
	        array[array.length] = allChildren[i]
	        array.length += 1
	    }
	}
	return array
	}
	zzdom.addClass = function (node,classes){
	  classes.forEach((value) => node.classList.add(value))
	}
	//调用
	zzdom.getSiblings(item3)
	zzdom.addClass(item3,['a','b','c'])
	
但是相比下，下面这种调用方法更好

	//调用
	item3.getSiblings(item3)
	item3.addClass(item3,['a','b','c'])
	
解决办法：更改`Node`原型

	Node.prototype.getSiblings = function (){ 
		var allChildren = this.parentNode.children 
		var array = { 
			length:0
		}
		for(let i = 0; i<allChildren.length; i++){
			if (allChildren[i] !== this){
				array[array.length] = allChildren[i]
				array.length += 1
			}
		}
		return array
		}
		Node.prototype.addClass = function (classes){
			classes.forEach((value) => this.classList.add(value))
	}
	//调用
	item3.getSiblings.call(item3)
	item3.addClass.call(item3,['a','b','c'])

> 注意：`this`是调用函数时的第一个参数。

上面代码弊端：如果之前声明过`getSiblings`和`addClass`，会被这次声明覆盖。
那么不更改原型，解决办法如下：

	window.jQuery = function (node){
		return{
		  getSiblings: function (){ 
			  var allChildren = node.parentNode.children 
			  var array = { length: 0 }
			  for(let i = 0; i<allChildren.length; i++){
			    if (allChildren[i] !== node){
			        array[array.length] = allChildren[i]
			        array.length += 1
			    }
			  }
			  return array
		  },
		  addClass: function (classes){
		    classes.forEach((value) => node.classList.add(value))
		  }
	   }
	}
	//调用
	var node2 = jQuery(item3)
	node2.getSiblings()
	node2.addClass(['a','b','c'])
	
增加类型检测：字符串`string`或选择器`selector`

	window.jQuery = function (nodeOrSelector){
		let node
		if(typeof nodeOrSelector === 'string'){
			node = document.querySelector(nodeOrSelector)
		}else{
			node = nodeOrSelector
		}
		
		return{
		  getSiblings: function (){ 
			  var allChildren = node.parentNode.children 
			  var array = { length: 0 }
			  for(let i = 0; i<allChildren.length; i++){
			    if (allChildren[i] !== node){
			        array[array.length] = allChildren[i]
			        array.length += 1
			    }
			  }
			  return array
		  },
		  addClass: function (classes){
		    classes.forEach((value) => node.classList.add(value))
		  }
	   }
	}
	//调用
	var node2 = jQuery('#item3')
	node2.getSiblings()
	node2.addClass(['a','b','c'])
	
#### `addClass`操作多个节点
	
	window.jQuery = function (nodeOrSelector){
		let nodes = {}
		if(typeof nodeOrSelector === 'string'){
		   //伪数组
		   nodes = document.querySelectorAll(nodeOrSelector)
		}else if(nodeOrSelector instanceof Node){
			//伪数组，保持返回结果一致
		    nodes = {
		        0: nodeOrSelector,
		        length: 1
		    }
		}
		return nodes
	}	
	//调用
	var node2 = jQuery('ul > li')
	console.log(node2)//__proto__:NodeList

加一个临时变量，去掉多余的原型链。

	window.jQuery = function (nodeOrSelector){
		let nodes = {}
		if(typeof nodeOrSelector === 'string'){
		    let temp=document.querySelectorAll(nodeOrSelector)
		    for(let i = 0; i<temp.length; i++){
		        nodes[i] = temp[i]
		    }
		    nodes.length = temp.length
		}else if(nodeOrSelector instanceof Node){
		    nodes = {
		        0: nodeOrSelector,
		        length: 1
		    }
		}			
		return nodes
	}	
	//调用
	var node2 = jQuery('ul > li')
	console.log(node2)//__proto__:Object 

添加`addClass`后代码如下

	window.jQuery = function (nodeOrSelector){
		let nodes = {}
		if(typeof nodeOrSelector === 'string'){
		    let temp=document.querySelectorAll(nodeOrSelector)
		    for(let i = 0; i<temp.length; i++){
		        nodes[i] = temp[i]
		    }
		    nodes.length = temp.length
		}else if(nodeOrSelector instanceof Node){
		    nodes = {
		        0: nodeOrSelector,
		        length: 1
		    }
		}	
		nodes.addClass = function(classes){
			classes.forEach((value)=>{
				for(let i=0; i<nodes.length; i++){
					nodes[i].classList.add(value)
				}
			})
		}	
		return nodes
	}	
	//调用
	var node2 = jQuery('ul > li')
	node2.addClass(['red'])//将所有`div`的`class`添加一个`red`

#### 添加`setText`

	window.jQuery = function (nodeOrSelector){
		let nodes = {}
		if(typeof nodeOrSelector === 'string'){
		    let temp=document.querySelectorAll(nodeOrSelector)
		    for(let i = 0; i<temp.length; i++){
		        nodes[i] = temp[i]
		    }
		    nodes.length = temp.length
		}else if(nodeOrSelector instanceof Node){
		    nodes = {
		        0: nodeOrSelector,
		        length: 1
		    }
		}	
		nodes.addClass = function(classes){
			classes.forEach((value)=>{
				for(let i=0; i<nodes.length; i++){
					nodes[i].classList.add(value)
				}
			})
		}	
		//`getText`获取文本
		nodes.getText = function(){
			var texts = []
			for(let i=0; i<nodes.length; i++){
				texts.push(nodes[i].textContent)
			}
			return texts
		}	
		//`setText`设置文本
		nodes.setText = function(text){
			for(let i=0;i<nodes.length; i++){
				nodes[i].textContent = text
			}
		}	
		return nodes
	}	
	var node2 = jQuery('ul > li')
	node2.addClass(['red'])//将所有`div`的`class`添加一个`red`
	node2.setText('hi')//将所有`div`的`textContent`改为`hi`

但是，对于`jQuery`来说，非常讨厌写`set`和`get`。更改如下：

		window.jQuery = function (nodeOrSelector){
		let nodes = {}
		if(typeof nodeOrSelector === 'string'){
		    let temp=document.querySelectorAll(nodeOrSelector)
		    for(let i = 0; i<temp.length; i++){
		        nodes[i] = temp[i]
		    }
		    nodes.length = temp.length
		}else if(nodeOrSelector instanceof Node){
		    nodes = {
		        0: nodeOrSelector,
		        length: 1
		    }
		}	
		nodes.addClass = function(classes){
			classes.forEach((value)=>{
				for(let i=0; i<nodes.length; i++){
					nodes[i].classList.add(value)
				}
			})
		}	
		nodes.text = function (text){
			if(text === undefined){
				var texts = []
				for(let i=0; i<nodes.length; i++){
			     texts.push(nodes[i].textContent)
		      }
			   return texts
		   }else{
				for(let i=0;i<nodes.length; i++){
				nodes[i].textContent = text
			}
		  }	
		}
		return nodes
	}	
	var node2 = jQuery('ul > li')
	node2.addClass(['red'])//将所有`div`的`class`添加一个`red`
	node2.text('hi')//将所有`div`的`textContent`改为`hi`
	
----
参考：[写代码啦] (https://xiedaimala.com/)