---
title: CSS 选择器
date: 2017-12-18 14:28:38
categories: CSS
tags:
---

##### 通用选择器：
	*{}
	//匹配所有元素
	
##### 标签选择器：
	h1{}
	
##### 类选择器：
	.name{}
	//匹配所有类名为 name 的元素
	
##### ID选择器：
	#name{}
	//匹配所有 ID 名为 name 的元素
	
##### 属性选择器：
	[target = blank]
	//匹配所有以 target 命名，值为 blank 的元素
	
##### 后代选择器：
	.header .box{}
	//匹配由 .header 作为祖先元素(但不一定是父元素)的后代元素 .box
	
##### 子选择器：
	.content > .title{}
	 //匹配由 .content 作为父元素的直接后代(子元素) .title
	
##### 即..又 选择器：
	.header.active{}
	//同时匹配 .header 和 .active , 一般会忽略前一个 class。
	
##### 多标签选择器：
	p1,span{} 
	//同时匹配 p1 和 span ，样式作用于两者。

##### 选择相邻的下一个：
	div+p{}
	//匹配所有紧接着`<div>`元素之后的`<p>`元素
	
##### 选择所有同级的邻居：
	div~p{}
	//匹配所有父级是`<div>`元素的`<p>`元素

##### 伪类：
	#header:hover{}
	//CSS3中的标准是伪类使用单冒号“:” 
	
##### 伪元素：
	#header::before{}
	//CSS3中的标准是伪元素使用双冒号“::”（避免和伪类混淆） 
	
#### CSS的继承、重要性

##### 继承
如果后代元素没有定义样式，那么会继承祖先元素的样式。

HTML

	<p>我是<span>谁</span></p>

如下代码，当只设置`p`的样式时，`span`里的文本会相应为蓝色。

	p{color: blue;}
	
这里分为可继承和不可继承的样式

	可继承的样式： font-size font-family color, UL LI DL DD DT;
	不可继承的样式：border padding margin width height ;
	
##### inherit 关键字
显式指定一个属性继承祖先元素的值，可用于继承性/非继承性属性。

##### 重要性`!important` 
当在一个样式声明中加上`!important`时，此声明将覆盖任何其他声明。
   
	p{color:red !important;}//这个会被应用
	p{color:green;}
	
>注意：应该尽量避免使用`!important`，因为这破坏了样式表中的固有的级联规则 使得调试找bug变得更加困难了。	


￼

	


	
	
		
	
	


		
			
		
	
	
	
	
