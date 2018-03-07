---
title: CSS 布局套路
date: 2017-12-16 19:08:02
categories: CSS
tags:
---

#### 元素的高度由什么决定？
`block`元素的高度由其内部文档流元素的高度总和决定，文档流是指文档内元素的流动方向。

	* inline 元素从左往右，如遇到宽度不够就另起一行。
	* block 元素从上往下另起一行。

	1.如果 div 里面只有一行 inline 元素，那么 div 的高度就是 inline 这一行的行高（文字的居中是基线对齐，不同文字行高不同，可以设定 line-hight 规定它）
	2.如果 div 里面有多行 inline 元素，div 高度是这多行加起来的行高。
	3.如果一个 div 里面有 div，那么这个 div 的高度由里面的 div 高度加 padding 加 margin（加 margin 分情况）

---

#### 布局原则

	* 尽量不要写固定 width 和 height 
	* 尽量用高级语法，如 calc flex 
	* 如果是 IE ，就全部写固定

---

#### `float`浮动布局（支持`IE8`）
	
	* 子元素加 float: left; 或 float: right;
	* 父元素加 .clearfix{content:''; display: block; clear: both;}
	.clearfix{zoom: 1;} //支持IE6
    
#### `flex`弹性布局（兼容`chorme` `mobile`，不支持`IE8`）
    * 父元素加 display: flex; justify-content: space-between;

---
			   
#### 水平居中
##### `child`为不定宽`block`元素（`parent`定宽/不定宽）。
	
	//方法一：转为 inline 元素
	child{display: inline;}
	parent{text-align: center;}

<img src="https://i.loli.net/2018/03/06/5a9e14649f84f.png
">
	
	//方法二：利用 table 长度自适应性，可将其看为定宽 block 元素
	child{display: table; margin-left/right: auto;}

<img src="https://i.loli.net/2018/03/06/5a9e149d8d3cd.png
">
	
	//方法三：margin 左右设同等值
	child{margin-left/right: 20px;}

<img src="https://i.loli.net/2018/03/06/5a9e14a9cc850.png
">
	
	//方法四：translateX -50%
	child{position: absolute; left: 50%; transform: translateX(-50%);}
	parent{position: relative;}

<img src="https://i.loli.net/2018/03/06/5a9e14b574741.png
">

##### `child`为定宽`block`元素（`parent`定宽/不定宽）

	child{width: 100px; margin-left/right: auto;}
	
<img src="https://i.loli.net/2018/03/06/5a9e15dcedb08.png
">
	
##### `inline` `inline-block`元素以及图片（`parent`定宽/不定宽）

	parent{text-align: center;}

<img src="https://i.loli.net/2018/03/06/5a9e17442bbb0.png
">
	
##### 通用方法（`flex`布局）
	
	parent{display: flex; justify-content: center;}	
---
	
#### 垂直居中
##### `child`为定高/不定高`block`元素（`parent`定高）
	
	//方法一：translateY -50%
	child{position: absolute; top: 50%; transform: translateY(-50%);}
	parent{position: relative;}

<img src="https://i.loli.net/2018/03/06/5a9e2fa910efa.png
">
	
	//方法二：利用 table (包括tbody、tr、td)标签。兼容IE。
	parent{vertical-align: middle;}
	
<img src="https://i.loli.net/2018/03/06/5a9e3071251c7.png
">
	
	//方法三：absolute + margin-top/bottom: auto;
	
<img src="https://i.loli.net/2018/03/06/5a9e2f5537c2a.png
">	

	//方法四
	child{ top: 50%; margin-top: 50%;}
	
<img src="https://i.loli.net/2018/03/06/5a9e2febcafc7.png
">	

##### `child`为`inline`单行文本以及图片（`parent`定高）

	//容器 height 和 line-height 设同等值
	parent{height: 40px; line-height: 40px;}
	
<img src="https://i.loli.net/2018/03/06/5a9e3936c4314.png
">	

##### `child`为`inline`多行文本以及图片（`parent`定高）

	//方法一：利用 table (包括tbody、tr、td)标签。兼容IE。
	parent{vertical-align：middle;}

<img src="https://i.loli.net/2018/03/06/5a9e394b3e99d.png
">

	//方法二：display: table-cell;
	parent{display: table-cell; vertical-align: middle;}

<img src="https://i.loli.net/2018/03/06/5a9e3962ba2c6.png
">

通用方法（`flex`布局）
	
	parent{display: flex; align-items: center;}

---

#### 左右布局

￼`float`实现

<img src="https://i.loli.net/2018/03/06/5a9e1b861d6bd.png
">
	
￼`flex`实现

<img src="https://i.loli.net/2018/03/06/5a9e1b7606c05.png
">

---
	                                                                
#### 平均布局
￼`float`实现

<img src="https://i.loli.net/2018/03/06/5a9e1a0475fa7.png
">

￼`flex`实现

<img src="https://i.loli.net/2018/03/06/5a9e1a15e92b7.png
">

---

#### 其他

##### 单行文本超出部分变成省略号

<img src="https://i.loli.net/2018/03/06/5a9e2006ebd58.png
">

##### 多行文本超出部分变成省略号

<img src="https://i.loli.net/2018/03/06/5a9e2023eee7d.png
">

##### 姓名 与 联系方式 两端对齐

<img src="https://i.loli.net/2018/03/06/5a9e1c7c9a4d8.png
">

---

参考：[写代码啦](https://xiedaimala.com/)




