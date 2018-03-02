---
title: DOM 常用API
date: 2017-12-30 20:47:31
categories: JavaScript
tags:
---

##### `DOM` 理解
	DOM（Document Object Model）是一棵树，树上有 Node ，Node 是一个构造函数（object 的一种）。
	Node 分为 Document（html）、Element（标签）和 Text（文本），以及其他不重要的 Attribute（属性）、Comment（注释）。
	
	* Document：XML(HTML 是 XML 的衍生品)
	* Element：节点对象代表文档树中的一个节点。
	* Text：模型

------

##### `DOM` 主要功能
	页面中的节点通过构造函数构造出对应的对象，这也叫 DOM API。￼
	
------	
	
##### 节点的类型
`DOM`的最小组成单位叫做节点`node`。文档的树形结构（`DOM`树），就是由各种不同类型的节点组成。每个节点可以看作是文档树的一片叶子。
`HTML DOM`节点的类型有七种。

	* Document：整个文档（DOM树的根节点），nodeType = 9
	* DocumentType：文档类型节点（比如<!DOCTYPE html>），nodeType = 10
	* Element：网页的各种HTML标签（比如<body>、<a>等），nodeType = 1
	* Attribute：网页元素的属性（比如class="right"），nodeType = 2
	* Text：标签之间或标签包含的文本，nodeType = 3
	* Comment：注释，nodeType = 8
	* DocumentFragment：文档的片段，nodeType = 11

这七种节点都属于浏览器原生提供的节点对象的派生对象，具有一些共同的属性和方法。

------

#### `Node` 接口
##### 属性

	* childNodes 获取子节点（可以是文本、注释、属性） 
	* children 获取子标签节点 
	* firstChild 返回第一个子节点
	* lastChild 返回最后一个子节点     
	* nextSibling 返回给定节点的下一个子节点 
	* previousSibling 返回给定节点的上一个子节点 
	* parentNode （w3c标准）返回给定节点的父节点
	* parentElement （只ie支持）返回给定节点的父标签
	* ownerDocument 返回元素的根节点文档对象（即 document 对象）
	* innerText 里面的文本
	* textContent 
	 
	* nodeName 节点的名称
		标签节点的 nodeName 是标签名称
		属性节点的 nodeName 是属性名称
		文本节点的 nodeName 永远是 #text
		文档节点的 nodeName 永远是 #document
	* nodeType 节点的类型     
	* nodeValue 节点的值
		文本节点的 nodeValue 属性包含文本。
		属性节点的 nodeValue 属性包含属性值。
		nodeValue 属性对于文档节点和标签节点是不可用的。
		
	注意：
	* nodeName 只有 svg 是小写，其他是大写
	* nextSibling 可能获取到文本
	* innerText 和 textContent 区别 	

##### 方法
如果一个属性是函数，那么这个属性就也叫做方法；换言之，方法是函数属性

	* appendChild() 将指定的节点添加到调用该方法的节点的子元素的末尾
	* removeChild() 删除指定的子节点并返回
	* replaceChild() 交换儿子（将另一个替换这一个，另一个去了内存）
	* cloneNode() 复制一个节点
	* insertBefore 添加一个节点到一个参照节点之前
	
	* contains() 一个元素是否包含另一个元素
	* hasChildNodes() 一个元素是否有儿子
	
	* isEqualNode() 是否相等（看起来一样）  
	* isSameNode() 是否相同（真的一样，等价于 ===）
	
	* normalize() 常规化，把不正常的变成正常的

	注意：
	1.cloneNode() 分为深拷贝和浅拷贝
	2.isEqualNode() 和 isSameNode() 区别
	 
------

#### `Document` 接口（查询接口，因为一般从 document 开始查）
##### 属性
 
	* characterSet 字符编码，比如‘UTF-8’
	* childElementCount 子元素的数量 
	* domain 域名
	* links 所有 a 标签
	* location 文档的 URL 相关的信息
	* onxxxxxxxxx 事件监听，比如 onclick 
	* origin 源
	* plugins 是否安装插件 
	* referrer 引荐

##### 方法

	* open() document步骤1.打开
	* close() document步骤3.关闭文档
	* write() document步骤2.（尽量不用write，用的话避免有延时性）
	* writeln() 写一行
	
	* createDocumentFragment() 创建一个 DocumentFragment，主要是用于添加大量节点到文档中时会使用到 
	* createElement() 创建元素
	* createTextNode() 创建文本节点
	
	* getElementById() 通过 id 获取元素
	* getElementsByClassName() 通过 className 获取元素
	* getElementsByName() 通过 name 获取元素，它返回一个即时的NodeList 对象。
	* getElementsByTagName() 通过 TagName 获取元素，比如 p button
	* getSelection() 获取用户选中的文本
	* querySelector() 通过选择器，返回一个元素
	* querySelectorAll() 通过选择器，返回多个元素组成的数组（一个元素也返回数组） 
		
	注意：
	1.获取元素主要使用 querySelector()、querySelectorAll() 
           
------
         
#### `Element` 的接口
`DOM API`获取的`Elements`都是伪数组
##### 属性

	* children 子元素列表
	* childElementCount 子元素数量
	* firstElementChild 第一个子元素
	* lastElementChild 最后一个子元素
	
	* classList 类名列表（对象）
	* className 类名（字符串）
	* id 元素id
	
	* attributes 所有显性属性
	* innerHTML 获取从对象的起始位置到终止位置的全部内容,不包括 Html 标签。
	
	* clientWidth 内容区 + padding 的宽度
	* clientHeight 内容区 + padding 的高度
	* scrollHeight 元素中可以滚动的高度
	* scrollWidth 元素中可以滚动的宽度
	* scrollTop 元素中的内容已经向上滚出去多少
	* scrollLeft 元素中的内容已经向左滚出去多少
	
##### 方法	

	* setAttribute() 设置或者改变指定属性并指定值
	* getAttribute() 返回指定元素的属性值
	* removeAttribute() 从元素中删除指定的属性
	* getElementsByClassName() 根据元素的 class 属性获取所有元素

----

