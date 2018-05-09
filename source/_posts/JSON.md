---
title: JSON
date: 2018-03-30 18:49:42
categories: JavaScript
tags:
---

#### `JSON`

	* JSON 是 JavaScript Object Notation 的简称。
	* 它是一种表示结构化数据的格式，通常用于服务端向网页传递数据。
	* 相比 XML，JSON 是在 JavaScript 中读写结构化数据的更好的方式。主要是因为 JSON 比 XML 更小、更快、更易解析。

##### `XML`

	* 曾有一段时间，XML 是互联网上传输结构化数据的事实标准。
	* 但是 XML 过于烦琐、冗长。为解决这个问题，涌现了一些方案。直到 2006年，Douglas Crockford 提出了 JSON 语言。

```	    
// nodejs（XML）
}else if(path === '/xxx'){
 response.statusCode = 200
 response.setHeader('Content-Type', 'text/XML')
 response.write(`
<note>
  <to>糖糖</to>
  <from>照照</from>
   <heading>hellow你好吗</heading>
   <body>hellow你好吗衷心感谢珍重再见期待再相逢</body>
 </note>
 `)
 response.end()
}
```

上面代码用 `JSON` 表示，如下：
	
```   
// nodejs（JSON）
}else if(path === '/xxx'){
 response.statusCode = 200
 response.setHeader('Content-Type', 'text/XML')
 response.write(`
  {
     "note":{
        "to": "糖糖",
        "from": "照照",
        "heading": "哈喽",
        "content": "你好吗"
      }
    }
 `)
 response.end()
}
```

##### `JSON` 与 `JavaScript` 的关系

	JSON 和 JavaScript 是两种不同的语法，JSON 参考了 JavaScript 。

##### `JSON` 与 `JavaScript` 的区别

	1. JSON 没有 function 和 undefined 。
	2. JSON 字符串首尾必须使用双引号。
		var code = '"\u2028\u2029"';
		JSON.parse(code);  // 正常
		eval(code);  // 错误
	3. JSON 中对象的属性名必须加双引号。一个对象以 { 开始并以 } 结束。最后一个属性后不能有逗号。		 
	4. JSON 的数组的属性名必须加双引号，一个数组以 [ 开始并以 ] 结束。最后一个属性后不能有逗号。	
	5. JSON 中没有原型链。

`JSON`字符串:

	var str = '{"name": "zhao", "age": 18}'

`JSON`对象:

	var obj = {"name": "zhao", "age": 18}

`JSON`数组:

	var arr1 = ["name", 18, true]
	var arr2 = ["Tom": {"age": 19}, "Jerry": {"age": 18}]

---

### `JSON`方法

#### `JSON.parse()`

`JSON.parse()` 方法用于将一个 `JSON` 字符串转换为对象。

语法

	JSON.parse(text[, reviver])
	
	text //必需，一个有效的 JSON 字符串。
	reviver //可选，一个转换结果的函数，将为对象的每个成员调用此函数。

```
JSON.parse('{}');              // {}
JSON.parse('true');            // true
JSON.parse('"foo"');           // "foo"
JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
JSON.parse('null');            // null
```

使用 `reviver` 参数

	JSON.parse('{"p": 5, "q": 6}', (key, value) => {
	  return typeof value === 'number'? value * 2 : value;   
	})
	//{p: 10, q: 12}
	
	//或
	var text = '{"p": 5, "q": 6}'
	var obj = JSON.parse(text, (key, value) => {
	  return typeof value === 'number'? value * 2 : value;   
	})
	obj //{p: 10, q: 12}
	
	
#### `JSON.stringify()`

`JSON.stringify()` 将一个 `JavaScript` 值(对象或者数组)转换为一个 `JSON`字符串。
 
语法

	JSON.stringify(value[, replacer[, space]])
	
	value //必需，要转换的 JavaScript 值（通常为对象或数组）。
	replacer //可选。用于转换结果的函数或数组。
	space //可选，文本添加缩进、空格和换行符。
 
```
JSON.stringify({}) //'{}'
JSON.stringify(true) //'true'
JSON.stringify("foo") //'"foo"'
JSON.stringify([1,"false",false]) //'[1,"false",false]'
JSON.stringify({ x: 5 }) //'{"x":5}'
```
 
##### `toJSON` 方法

如果一个被序列化的对象拥有 `toJSON` 方法，那么该 `toJSON` 方法就会覆盖该对象默认的序列化行为：不是那个对象被序列化，而是调用 `toJSON` 方法后的返回值会被序列化，例如：

	var obj = {
	  foo: 'foo',
	  toJSON: function () {
	    return 'bar';
	  }
	};
	JSON.stringify(obj) //'"bar"'
	JSON.stringify({x: obj}) //'{"x":"bar"}'
	
---	
