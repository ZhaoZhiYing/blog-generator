---
title: JS 数据类型转换
date: 2018-02-14 20:45:49
categories: JavaScript
tags:
---

#### 转成 `String`
1.`string()`可以用于任何数据类型。该方法底层使用的也是 `toString()` 方法。转换规则如下：

	Number：转为相应的字符串。
		String(123) // "123"
		
	String：转换后还是原来的值。
		String('abc') // "abc"
		
	Boolean：true 转为字符串 "true"，false转为字符串"false"。
		String(true) // "true"
		
	undefined：转为字符串 "undefined"。
		String(undefined) // "undefined"
	
	null：转为字符串 "null"。
		String(null) // "null"
		
	String方法的参数如果是对象，返回一个类型字符串；如果是数组，返回该数组的字符串形式。
		String({a: 1}) // "[object Object]"
		String([1, 2, 3]) // "1,2,3"
	//这里先后隐式调用了 toString 和 valueOf 方法。	

##### `string()` 与 `toString()` 的区别

	* toString() 可以将所有的的数据都转换为字符串，但是要排除 null 和 undefined。
	* string() 可以将 null 和 undefined 转换为字符串，但是没法转进制字符串。

##### `toString` 与 `valueOf` 的区别 
`toString()` 方法返回一个表示该对象的字符串。

	语法：object.toString()

`valueOf()` 方法返回指定对象的原始值。

	语法：object.valueOf()

	Array 返回数组对象本身。
	Boolean 布尔值。
	Date	存储的时间是从 1970 年 1 月 1 日午夜开始计的毫秒数 UTC。
	Function 函数本身。
	Number 数字值。
	Object 对象本身。这是默认情况。
	String 字符串值。
	
	Math 和 Error 对象没有 valueOf 方法。
	
```
//1.调用情况
在数值运算里，会优先调用 valueOf()，如 a + b
在字符串运算里，会优先调用 toString()，如 alert(c)
	
//2.返回值类型
toString 一定将所有内容转为字符串。
valueOf 取出对象内部的值，不进行类型转换。

//3.用途
valueOf 专用于算数计算和关系运算。
toString 专用于输出字符串。
```

2.+ 空字符串
	
	123 + '' // "123"
	true + '' // "true"
	undefined + '' // "undefined"
	null + '' // "null"
	
	var obj = {}
	obj + '' // "[object Object]"

---

#### 转成 `Boolean`
1.`Boolean()` 可以用于任何数据类型。除了以下五个`falsy`值，其他的值全部为`true`。

	//falsy 是在 boolean 上下文中认定可转换为 false 的值
	
	Boolean(undefined) // false
	Boolean(null) // false
	Boolean(0) // false
	Boolean(NaN) // false
	Boolean('') // false 
		
		
2.任何数据取反两次都可以得到一个布尔值。

	//五个 falsy 值
	!!undefined // false
	!!null // false
	!!0 // false
	!!NaN // false
	!!'' // false
	
	//其他
	!![] // true
	!!{} // true
	!!123 // true

---

#### 转成 `Number`
1.`number()`可以用于任何数据类型。转换规则如下：
	
	* Boolean：true 和 false 分别转成 1 和 0
			Number(true) // 1
	
	* Number：简单传入和返回
			Number(5) // 5
	
	* Null：返回 0
	* undefined：返回 NaN
	
	* String
		如果可以被解析为数值，则转换为相应的数值
			Number('032') // 32
		如果不可以被解析为数值，返回 NaN（非数字）
			Number('abc') // NaN
		空字符串转为0	
			Number('') // 0
			
	* Object：返回 NaN，除非是包含单个数值的数组。
			Number({name: 'zhao'}) // NaN
			Number([1, 2, 3]) // NaN
			Number([1]) // 1
	//这里先后隐式调用了 valueOf 和 toString 方法。

2.`parsetInt()`函数解析一个字符串参数，并返回一个指定基数的整数。

	语法：parseInt(string, radix)
	
	parseInt("3.14") //3
	parseInt("3ff") //3
	parseInt("oo3") //3
	parseInt("") //十六进制
	parseInt("") //十进制
	parseInt("") //八进制
	parseInt("") //二进制
	


3.`parsetFloat()`解析一个字符串参数并返回一个浮点数。只解析十进制，因此无第二个参数。

	parseFloat("3.14") //3.14
	parseFloat("3.14.12") //3.14
	parseFloat("314e-2") //3.14
	parseFloat("0.0314E+2") //3.14
	parseFloat("3.14more") //3.14
	parseFloat("oo3.14") //NaN


4.自动转换

	'5' - '2' // 3
	'5' * '2' // 10
	true - 1  // 0
	false - 1 // -1
	'1' - 1   // 0
	'5' * []    // 0
	false / '5' // 0
	'abc' - 1   // NaN
	null + 1 // 1
	undefined + 1 // NaN
	
	+'abc' // NaN
	-'abc' // NaN
	+true // 1
	-false // 0
	
---	

参考：[阮一峰-数据类型转换](http://javascript.ruanyifeng.com/grammar/conversion.html#toc2)

