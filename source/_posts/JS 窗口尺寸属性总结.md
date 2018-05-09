---
title: JS 窗口尺寸属性总结
date: 2018-04-16 23:00:18
categories: JavaScript
tags:
---


	* Element.clientHeight //返回元素节点可见部分的高度。
		//clientheight = padding + height - 横向滚动轴高度。
	* Element.clientWidth //返回元素节点可见部分的宽度。
	* Element.clientLeft //返回元素节点左边框的宽度。
	* Element.clientTop //返回元素节点顶部边框的宽度。

---

	* Element.scrollHeight //返回元素节点的总高度。
		//scrollHeight = 可滚动高度，就是将滚动框拉直，不再滚动的高度。
	* Element.scrollWidth //返回元素节点的总宽度。
	* Element.scrollLeft //设置或返回位于对象左边界和窗口中目前可见内容的最左端之间的距离。
	* Element.scrollTop //设置或返回位于对象顶边界和窗口中目前可见内容的最顶端之间的距离。
	
---


	* Element.offsetHeight //返回元素的垂直高度(包含border,padding)。
		//offsetheight = padding + height + border + 横向滚动轴高度。
	* Element.offsetWidth //返回元素的水平宽度(包含 border,padding)。
	* Element.offsetParent //返回一个指向最近的（closest，指包含层级上的最近）包含该元素的定位元素。
	* Element.offsetLeft //返回当前元素左上角相对其 offsetParent 节点的左边界偏移的像素值。
	* Element.offsetTop //返回当前元素相对于其 offsetParent 元素的顶部的距离。

	
---	
	
	* screen.availHeight //可用的屏幕宽度（不包括 Windows 任务栏）
	* screen.availWidth //可用的屏幕高度（不包括 Windows 任务栏）
	* screen.height //返回屏幕的总高度
	* screen.width //返回屏幕的总宽度

	
---

	* window.innerHeight //浏览器窗口的视可高度(包括滚动条)
	    //IE 中 body 元素的 clientHeight 属性与该属性相同。
	* window.innerWidth // 浏览器窗口的视可宽度(包括滚动条)
	    //IE 中 body 元素的 clientWidth 属性与该属性相同。
	    
	
--- 

	* window.outerHeight //设置或返回一个窗口的外部高度，包括所有界面元素（如工具栏/滚动条）。
	* window.outerWidth //设置或返回窗口的外部宽度，包括所有的界面元素（如工具栏/滚动）。


---   