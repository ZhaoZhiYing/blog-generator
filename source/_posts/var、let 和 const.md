---
title: var、let 和 const
date: 2018-04-02 15:02:16
categories:
tags:
---


#### `ES3`声明

#### `a = 1` 

	1. 如果当前有 a ，就直接使用这个 a 。
	2. 如果没有，就声明一个全局变量 a 。
	
举例一

	var a 
	function foo(){
		a = 1
		console.log(window.a)
	}
	foo() // 1

举例二

	function foo(){
		a = 1
	}
	console.log(window.a) // 1 
	

#### `var a = 1`

	1. var 声明的变量会被提升。
	2. var 可以重复声明，后声明的覆盖前面。
	3. var 可以先声明，后赋值。

举例一

```
console.log(a)
var a = 2 
// undefined

//上面代码等于下面
var a
console.log(a)
a = 1  

//var 声明会在代码执行之前 创建变量，并将其初始化为 undefined  
```

举例二

	(function (){
			var a = 1
			window.foo = function(){
				console.log(a)
			}
	}())
	
	//undefined
	

#### `ES6`声明

#### `let a = 1`

	1. let 声明的变量不会被提升。
	2. let 必须先声明再使用。
	3. let 不能重复声明。

举例一

	{
		console.log(a)
		let a = 1		
	}
	
	// a is not defined

	
	
举例二
	
	{
		let a = 1
		console.log(a)
		let a = 2
		console.log(a)
	}
	// Identifier 'a' has already been declared


#### `	const a = 1`

`const` 用法同 `let`，不同的是 `const` 只有一次赋值机会，且必须在声明的时候赋值。

举例一

```
{
	const a = 1
	console.log(a)
	a = 2
	console.log(a)
}
// Assignment to constant variable
```

---

#### 相关问题

	var liTags = document.querySelectorAll('li') 
	
	//liTags.length 为 5
	for(var i=0; i<liTags.length; i++){ 
		liTags[i].onclick = function(){
			console.log(i)
		}
	}
	
	//当点击任意 li 时，打印值都为 5

那么，如果对应打印出 `0 1 2 3 4`

	var liTags = document.querySelectorAll('li') 
	
	//liTags.length 为 5
	for(var i=0; i<liTags.length; i++){ 
		(function(j){
			liTags[j].onclick = function(){
				console.log(j)
			}
		})(i)
	}

	//点击对应 li 会依次打印出 0 1 2 3 4

相比下，使用 `let` 容易很多。

	var liTags = document.querySelectorAll('li') 
	
	//liTags.length 为 5
	for(var i=0; i<liTags.length; i++){ 
		let j = i
		liTags[j].onclick = function(){
			console.log(j)
		}
	}
	
	//let j = i 不会被提升为全局变量，点击对应 li 会依次打印出 0 1 2 3 4
	
另外，有一种写法。

	for(let i=0; i<liTags.length; i++){ 
		liTags[j].onclick = function(){
			console.log(j)
		}
	}	
	
	//JS 引擎会自动完成下面操作，并产生 7 个 i 
	for(let i=0; i<liTags.length; i++){  //()作用域里有一个 i
		//{} 块里面的 i = ()里的 i
		liTags[j].onclick = function(){
			console.log(j)
		}
		//到这里时，()里的 i = {} 块里面的 i
	}

---
