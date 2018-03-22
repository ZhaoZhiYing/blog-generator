---
title: JS 数组
date: 2018-02-20 17:13:10
categories: JavaScript
tags:
---

#### 什么是数组
人类理解：数组就是数据的有序集合（每个值的位置都有索引（从0开始））
JS理解：数据就是原型链中有 `Array.prototype` 的对象。

---

#### 创建数组
1.使用 `Array` 构造函数。
  
	var arr = new Array(8) //创建 length 为 8 的数组。
	var arr = new Array('red', 'blue', 'green') //创建了包含3个字符串的数组
	
	//new 操作符可省略，上面代码同等于下：
	var arr = Array(8) 
	var arr = Array('red', 'blue', 'green') 
	
2.数组字面量	
	
	//创建了包含3个字符串的数组
	var arr = ['red', 'blue', 'green']
	
	//除了在定义时赋值，数组也可以先定义后赋值。
	var arr = []
	arr[0] = 'a'
	
	//数组可以保存任何类型的数据。
	var arr = [
	  {a: 1},
	  [1, 2, 3],
	  function() {return true;}
	]
	arr[0] // Object {a: 1}
	
	//如果数组的元素还是数组，就形成了多维数组。
	var a = [[1, 2], [3, 4]]
	a[0][1] // 2 
	a[1][1] // 4

---

#### `length` 属性
数组的`length`属性是可写的，如下：

	var arr = ['red', 'blue', 'green']
	arr.length = 4 
	arr[3] // undefined 

	var arr = ['red', 'blue', 'green']
	arr.length = 2 // 这里删除了 arr[2]
	arr[2] // undefined 
	
	var arr = ['red', 'blue', 'green']
	arr[3] = 'gray' //这里增加了一项
	arr.length // 4

---

#### 检测数组
##### `instanceof` 和 `isArray`

`instanceof`语法
	
	object instanceof constructor
	//object 要检测的对象
	//constructor 某个构造函数
	
	//如下	
	var obj = []
	obj instanceof Array //true
	
`isArray`语法
	
	Array.isArray(obj) //obj 需要检测的值
	
	//如下
	var obj = Array(1,2,3)
	Array.isArray(obj) //true
	
	Array.isArray([1,2,3]) //true

>在浏览器中，我们的脚本可能需要在多个窗口之间进行交互。多个窗口意味着多个全局环境，不同的全局环境拥有不同的全局对象，从而拥有不同的内置类型构造函数。

这时当检测`Array`实例时，`Array.isArray` 优于 `instanceof`,因为`Array.isArray`能检测`iframes`。

举例
	
	var iframe = document.createElement('iframe')
	document.body.appendChild(iframe)
	
	arr1 = window.frames[window.frames.length-1].Array
	var arr2 = new arr1(1,2,3) // [1,2,3]
	
	
	Array.isArray(arr) // true
	arr instanceof Array // false

---

#### 伪数组（类数组）
* 有 0,1,2,3,4,5...n,length 这些 key 的对象
* 原型链中没有 `Array.prototype`。或者说没有 `push` 方法。

比如函数的`argument`参数，还有像调用`getElementsByTagName` `document.childNodes`之类的，它们都返回`NodeList`对象都属于伪数组。

伪数组转成真数组方法 
    
    var arr = Array.prototype.slice.call(fakeArray)
    //fakeArray 表示一个伪数组
    
举例

	var fakeArray = {0:'a',1:'b',length:2} //伪数组
	var arr1 = Array.prototype.slice.call(fakeArray)
	arr1[0] //"a"	
	//或者
	var arr2 = [].slice.call(fakeArray) 
	arr2[0] //"a"

---

#### 数组的 `API`

##### 1.`join()`

一个参数：以参数作为分隔符，将所有数组成员组成一个字符串返回。如果不提供参数，默认用逗号分隔。`undefined`或`null`或空位，会被转成空字符串。

	[1, 2, 3].join('#')
	//"1#2#3"
	
	[1, 2, 3].join()
	//"1,2,3"

	[undefined, null].join('-')
    //"-"

    
##### 2.`concat()` 
 
用于合并两个或多个数组。它将新数组的成员，添加到原数组成员的后部，返回一个新数组，原数组不变。

参数：除了接受数组作为参数，`concat`也可以接受其他类型的值作为参数。
                         
	//合并多个数组
	var a = ['a', 'b', 'c']
	var b = [1, 2, 3]
	a.concat(b);
	//["a", "b", "c", 1, 2, 3]
	
	//复制一个数组，浅拷贝。
	var a = [1, 2, 3]
	var b = a.concat([]) 
	b // [1, 2, 3]

  	 	  
##### 3.`slice()`

用于提取原数组的一部分，返回一个新数组，原数组不变。

两个参数：第一个参数为起始位置（从0开始）。第二个参数为终止位置（但该位置的元素本身不包括在内）。

	var a = ['a', 'b', 'c'];
	a.slice(1, 2) // ["b"]

##### 4.`map()`

创建一个新数组，其结果是该数组中的每个元素(按照原始数组元素顺序)都调用一个提供的函数后返回的结果。同`forEach()`一样，但有返回值。

一个参数：参数是一个函数。该函数有三个参数：当前位置的值`element`、当前位置的编号`index`、整个数组`array`

	var a = [1, 2, 3]
	a.map(function(n){
	   return n + 1
	})
	//[2, 3, 4]
	
	[1, 2, 3].map(function(ele, i, arr) {
		return ele * i
	})
	//[0, 2, 6]
	
	
##### 5.`forEach()`

同`map()`一样，但没有返回值。

	var foo = [1, 2, 3]
	foo.forEach(function(ele,i){
		console.log(ele * i)
	})
              
##### 6.`filter()` 
 
用于过滤数组成员，满足条件的成员组成一个新数组返回。

一个参数：是一个函数，所有数组成员依次执行该函数，返回结果为`true`的成员组成一个新数组返回。

	[1, 2, 3, 4, 5].filter(function (elem){
	  	return (elem > 3)
	})
	//[4, 5]


##### 7.`reduce()` `reduceRight()`

依次处理数组的每个成员，最终累计为一个值。

两个参数：第一个参数是一个函数，该函数必须接受两个参数: 之前的结果、当前变量；第二个参数是当前的初值。

	[1, 2, 3, 4, 5].reduce(function(x, y){
		return x + y
	})
	//15
	
	//计算所有基数的和
	var a = [1,2,3,4,5,6,7,8,9]
	a.reduce((sum,n) => { 
		return n%2 === 1 ? sum+n:sum 
	},0)
	//25
	
难点1.`map` 可以用 `reduce` 表示

	a = [1, 2, 3] 
	a.reduce(function(arr, n){
			arr.push(n*2)
			return arr
	},[])
	// [2, 4, 6]

难点2.`filter` 可以用 `reduce` 表示

	a = [1, 2, 3, 4, 5, 6]
	a.reduce(function(arr, n){
		if(n % 2 === 0){
			arr.push(n) 		}
		return arr	
	},[]) 
	// [2, 4, 6]


##### 8.`sort()` 

对数组成员进行排序。排序后，原数组将被改变。

两个参数：表示进行比较的两个元素。

	[10, 12, 9].sort(function (a, b) {
	  return a - b;
	})
	// [0, 10, 12]
	//如果返回值大于0，表示第一个元素排在第二个元素后面；小于0，表示第一个元素排在第二个元素前面。其他情况 ，位置不变。


##### 9.`push()`

在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。该方法会改变原数组。

	var a = [];
		a.push(1) 
	//[1]                 

还可以用于向对象添加元素


##### 10.`pop()`

用于删除数组的最后一个元素，并返回该元素。该方法会改变原数组。

	var a = ['a', 'b', ‘c’];
	a.pop() // 'c'
                      
`push()`和`pop()`结合使用，就构成了“后进先出”的栈结构（stack）

##### 11.`unshift()`

用于在数组的第一个位置添加一个或多个元素，并返回添加新元素后的数组长度。该方法会改变原数组。

	var a = ['a', 'b', 'c'];
	a.unshift('x'); 
	a //['x', 'a', 'b', 'c']
	
	                      
##### 12.`reverse()`

用于颠倒数组中元素的顺序，返回改变后的数组。该方法会改变原数组。

	var a = ['a', 'b', 'c'];
	a.reverse() // ["c", "b", "a"]


##### 13.`splice()`

用于删除原数组的一部分成员，并可以在被删除的位置添加入新的数组成员，返回值是被删除的元素。该方法会改变原数组。

两个参数：第一个参数是删除的起始位置；第二个参数是被删除的元素个数。如果后面还有参数，则表示这些就是要被插入数组的新元素。

	var a = ['a', 'b', 'c', 'd', 'e', 'f'];
	a.splice(4, 2, 1, 1) 
	a 
	// ["a", "b", "c", "d", 1, 1]


##### 14.`some()` `every()`
 
用来判断数组成员是否符合某种条件。

一个参数：接受一个函数作为参数，所有数组成员依次执行该函数，返回一个布尔值。该函数接受三个参数：当前位置的值`element`、当前位置的编号`index`、整个数组`array`

两者区别如下：

	[1,2,3,4,5,6,7].some(function(ele){
		return ele > 3
	})
	//true
		
	[1,2,3,4,5,6,7].every(function(ele){
		return ele > 3
	})
	//false

##### 15.`indexOf()` `lastIndexOf()`

按原始顺序搜索数组中的元素，并返回它所在的位置。

两个参数：第一个参数表示要搜索的元素；第二个参数表示搜索的开始位置。

两者区别如下：

	['a', 'b', 'c'].indexOf('a', 1) 
	//-1 
	
	['a', 'b', 'c'].lastIndexOf('a', 1) 
	//0
	
无法确定数组成员是否包含`NaN`。因为这两个方法内部，使用严格相等运算符`===`进行比较，而`NaN`是唯一一个不等于自身的值。
	
	[1,2,NaN].indexOf(NaN) // -1
	[1,2,NaN].lastIndexOf(NaN) // -1
						      
---
    