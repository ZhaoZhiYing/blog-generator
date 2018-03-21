---
title: DOM 对象常用API
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

##### `DOM` 主要功能
	页面中的节点通过构造函数构造出对应的对象，这也叫 DOM API。￼
	
##### 节点的类型
`DOM`的最小组成单位叫做节点`node`。文档的树形结构（`DOM`树），就是由各种不同类型的节点组成。每个节点可以看作是文档树的一片叶子。
`HTML DOM`节点的类型有七种。

	* Document //整个文档（DOM树的根节点），nodeType = 9
	* DocumentType //文档类型节点（比如<!DOCTYPE html>），nodeType = 10
	* Element //网页的各种HTML标签（比如<body>、<a>等），nodeType = 1
	* Attribute //网页元素的属性（比如class="right"），nodeType = 2
	* Text //标签之间或标签包含的文本，nodeType = 3
	* Comment //注释，nodeType = 8
	* DocumentFragment //文档的片段，nodeType = 11

这七种节点都属于浏览器原生提供的节点对象的派生对象，具有一些共同的属性和方法。

------

#### `Node`
##### 节点属性   
	 
	* Node.nodeName //节点的名称。
	* Node.nodeType //节点的类型。     
	* Node.nodeValue //节点的值。
	* Node.textContent //返回或摄制组当前节点和它的所有后代节点的文本内容。
	* Node.baseURI //返回当前网页的绝对路径。
	
	* Node.ownerDocument //返回元素的根节点文档对象（即 document 对象）。  
	* Node.nextSibling //返回给定节点的下一个子节点。
	* Node.previousSibling //返回给定节点的上一个子节点。 
	* Node.parentNode //（w3c标准）返回给定节点的父节点。
	* Node.parentElement //（只ie支持）返回给定节点的父标签。
	* Node.childNodes //获取子节点（可以是文本、注释、属性）。  
	* Node.firstChild //返回第一个子节点。
	* Node.lastChild //返回最后一个子节点。	
	
	//parentNode接口	
	* parentNode.children //获取子标签节点。
	* parentNode.firstElementChild //返回当前节点的第一个 Element 子节点。
	* parentNode.lastElementChild //返回当前节点的最后一个 Element 子节点。
	* parentNode.childElementCount //返回当前节点所有 Element 子节点的数目。
	
	注意：
	* nodeName 只有 svg 是小写，其他是大写。
	* nextSibling 可能获取到文本。

##### 方法（如果一个属性是函数，那么这个属性就也叫做方法；换言之，方法是函数属性）

	* Node.appendChild(node) //向节点末尾添加一个子节点。
	* Node.removeChild(node) //删除子节点，在要删除节点的父节点上操作。
	* Node.replaceChild(newChild,oldChild) //替换节点。
	* Node.cloneNode() //复制节点。
		语法：var dupNode = 被克隆节点.cloneNode(deep);
		//deep 是否深拷贝，默认为 false ，浅拷贝只克隆节点。
	   //如果为 true ，深拷贝克隆节点和属性，以及后代。

	* Node.insertBefore(newNode,oldNode) //在指定子节点之前插入新的子节点。
	* Node.contains(node) //返回一个布尔值，表示参数节点是否为当前节点的后代节点。
	* Node.hasChildNodes() //返回布尔值，表示当前节点是否有子节点。
	* Node.isEqualNode() //返回布尔值，用于检查两个节点是否相等。
	* Node.isSameNode() //返回布尔值，用于检查两个节点是否相同（等价于 ===）。
	* Node.normalize() //用于清理当前节点内部的所有 Text 节点。它会去除空的文本节点，并且将毗邻的文本节点合并成一个。

	//ChildNode接口
	* ChildNode.remove() //用于删除当前节点。
	* ChildNode.before() //在这个节点的前面插入节点（同父节点）。
	* ChildNode.after() //在这个节点的末尾插入节点（同父节点）。
	* ChildNode.replaceWith() //替换当前节点父节点下的子节点。 
	
	注意：
	1.cloneNode() 分为深拷贝和浅拷贝。
	 
------

#### `Document`（查询接口，因为一般从 document 开始查）
##### 属性
 
	* document.documentElement //返回当前文档的根节点。
	* document.defaultView //返回 document 对象所在的 window 对象。
	* document.body //返回当前文档的 <body> 节点。
	* document.head //返回当前文档的 <head> 节点。
	* document.activeElement //返回当前文档中获得焦点的那个元素。
	
	//节点集合属性
	* document.links //返回当前文档的所有 a 元素。
	* document.forms //返回页面中所有表单元素。
	* document.images //返回页面中所有图片元素。
	* document.embeds //返回网页中所有嵌入对象。
	* document.scripts //返回当前文档的所有脚本。
	* document.styleSheets //返回当前网页的所有样式表。
	
	//文档信息属性
	* document.documentURI //表示当前文档的网址。
	* document.URL //返回当前文档的网址。
	* document.domain //返回当前文档的域名。
	* document.lastModified //返回当前文档最后修改的时间戳。
	* document.location //返回 location 对象，提供当前文档的 URL 信息。
	* document.referrer //返回当前文档的访问来源。
	* document.title //返回当前文档的标题。
	* document.characterSet //属性返回渲染当前文档的字符集，比如UTF-8、ISO-8859-1。
	* document.readyState //返回当前文档的状态。
	* document.designMode //控制当前文档是否可编辑，可读写。
	* document.compatMode //返回浏览器处理文档的模式。
	* document.cookie //用来操作 Cookie。

##### 方法

	//读写
	* document.open() //用于新建并打开一个文档。
	* document.close() //关闭 open 方法所新建的文档。
	* document.write() //用于向当前文档写入内容（尽量不用 write，用的话避免有延时性）。
	* document.writeln() //用于向当前文档写入内容，尾部添加换行符。
	
	//生成节点
	* document.createElement(tagName) //创建一个元素节点。
	* document.createTextNode(text) //创建一个文本节点。
	* document.createAttribute(name) //创建一个属性对象节点，并返回它。
	* document.createDocumentFragment() //创建一个DocumentFragment 对象。
	
	//查找节点
	* document.querySelector(selectors) //接受一个 CSS 选择器作为参数，返回第一个匹配该选择器的元素节点。
	* document.querySelectorAll(selectors) //接受一个 CSS 选择器作为参数，返回所有匹配该选择器的元素节点。
	* document.getElementsByTagName(tagName) //返回所有指定 HTML 标签的元素。
	* document.getElementsByClassName(className) //返回包括了所有class名字符合指定条件的元素。
	* document.getElementsByName(name) //用于选择拥有 name 属性的 HTML 元素（比如 <form>、<radio>、<img>、<frame>、<embed> 和<object> 等）。
	* document.getElementById(id) //返回匹配指定 id 属性的元素节点。
	* document.elementFromPoint(x,y) //返回位于页面指定位置最上层的 Element 子节点。 

	//其他
	* document.hasFocus() //返回一个布尔值，表示当前文档之中是否有元素被激活或获得焦点。
	* document.adoptNode(externalNode) //将某个节点，从其原来所在的文档移除，插入当前文档，并返回插入后的新节点。
	* document.importNode(externalNode, deep) //从外部文档拷贝指定节点，插入当前文档。
		
	注意：
	1.获取元素主要使用 querySelector()、querySelectorAll() 
           
------
         
#### `Element`
`DOM API` 获取的 `Elements` 都是伪数组。

##### 属性

	//特性属性
	* Element.attributes //返回当前元素节点的所有属性节点。
	* Element.id //设置或返回指定元素的 id。
	* Element.tagName //返回元素的标签名。
	
	* Element.innerHTML //设置或返回位于对象起始和结束标签内的 HTML(标签和文本)。
	* Element.outerHTML //设置或返回对象及其内容的 HTML(标签和文本)。
	* Element.innerText //设置或获取位于对象起始和结束标签内的文本(只兼容IE)。
	* Element.outerText //设置(包括标签)或获取(不包括标签)对象的文本 。
	
	* Element.className //返回或设置当前元素的 class 属性。
	* Element.classList //返回当前元素节点的所有 class 集合。
	* Element.dataset //返回元素节点中所有的 data-* 属性。
	
	//尺寸属性
	* Element.clientHeight //返回元素节点可见部分的高度。
		//clientheight = padding + height - 横向滚动轴高度。
	* Element.clientWidth //返回元素节点可见部分的宽度。
	* Element.clientLeft //返回元素节点左边框的宽度。
	* Element.clientTop //返回元素节点顶部边框的宽度。
	* Element.scrollHeight //返回元素节点的总高度。
		//scrollHeight = 可滚动高度，就是将滚动框拉直，不再滚动的高度。
	* Element.scrollWidth //返回元素节点的总宽度。
	* Element.scrollLeft //返回元素节点的水平滚动条向右滚动的像素数值,通过设置这个属性可以改变元素的滚动位置。
	* Element.scrollTop //返回元素节点的垂直滚动向下滚动的像素数值。
	* Element.offsetHeight //返回元素的垂直高度(包含border,padding)。
		//offsetheight = padding + height + border + 横向滚动轴高度。
	* Element.offsetWidth //返回元素的水平宽度(包含 border,padding)。
	* Element.offsetLeft //返回当前元素左上角相对于  HTMLElement.offsetParent 节点的左边界偏移的像素值。	* Element.offsetParent //节点的垂直偏移。
	* Element.offsetTop //返回水平位移。
	* Element.style //返回元素节点的行内样式。
	
	//节点相关属性
	* Element.children //包括当前元素节点的所有子元素。
	* Element.childElementCount //返回当前元素节点包含的子 HTML 元素节点的个数。
	* Element.firstElementChild //返回当前节点的第一个 Element 子节点。  
	* Element.lastElementChild //返回当前节点的最后一个 Element 子节点。  
	* Element.nextElementSibling //返回当前元素节点的下一个兄弟 HTML 元素节点。
	* Element.previousElementSibling //返回当前元素节点的前一个兄弟 HTML 节点。
	* Element.offsetParent //返回当前元素节点的最靠近的、并且 CSS 的 position 属性不等于 static 的父元素。
	
##### 方法	

	//位置方法
	* getBoundingClientRect() //返回一个对象，包含top,left,right,bottom,width,height（width、height 为元素自身宽高）。
		top //元素上外边界距窗口最上面的距离。
		right //元素右外边界距窗口最上面的距离。
		bottom //元素下外边界距窗口最上面的距离。
		left //元素左外边界距窗口最上面的距离。
		width //元素自身宽(包含 border,padding) 。
		height //元素自身高(包含 border,padding)。 
	* getClientRects() //返回当前元素在页面上形参的所有矩形。
	* Element.scrollIntoView() //滚动当前元素，进入浏览器的可见区域。
	
	//属性方法
	* Element.getAttribute() //读取指定属性。  
	* Element.setAttribute() //设置指定属性。  
	* Element.hasAttribute() //返回一个布尔值，表示当前元素节点是否有指定的属性。  
	* Element.removeAttribute() //移除指定属性。

	//查找方法
	* Element.querySelector()  
	* Element.querySelectorAll()  
	* Element.getElementsByTagName()  
	* Element.getElementsByClassName()

	//事件方法
	* Element.addEventListener() //添加事件的回调函数。  
	* Element.removeEventListener() //移除事件监听函数。  
	* Element.dispatchEvent() //触发事件。
	//IE8
	* Element.attachEvent(oneventName,listener)
	* Element.detachEvent(oneventName,listener)
	
	//解析 HTML 字符串，然后将生成的节点插入 DOM 树的指定位置。
	* Element.insertAdjacentHTML(where, htmlString); 
	* Element.insertAdjacentHTML('beforeBegin', htmlString); // 在该元素前插入。  
	* Element.insertAdjacentHTML('afterBegin', htmlString) // 在该元素第一个子元素前插入。 
	* Element.insertAdjacentHTML('beforeEnd', htmlString) // 在该元素最后一个子元素后面插入。 
	* Element.insertAdjacentHTML('afterEnd', htmlString) // 在该元素后插入。
	
	* Element.remove() //用于将当前元素节点从 DOM 中移除。
	* Element.focus() //用于将当前页面的焦点，转移到指定元素上。
	
----

