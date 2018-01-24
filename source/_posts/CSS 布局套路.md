---
title: CSS 布局套路
date: 2017-12-16 19:08:02
tags:
---
#### 元素的高度由什么决定？
`block`元素的高度由其内部文档流元素的高度总和决定，文档流是指文档内元素的流动方向。

	* inline 元素从左往右，如遇到宽度不够就另起一行。
	* block 元素从上往下另起一行。

	1.如果 div 里面只有一行 inline 元素，那么 div 的高度就是 inline 这一行的行高（文字的居中是基线对齐，不同文字行高不同，可以设定 line-hight 规定它）
	2.如果 div 里面有多行 inline 元素，div高度是这多行加起来的行高。
	3.如果一个 div 里面有div，那么这个div的高度由里面的div高度加 padding 加 margin（加margin分情况）

#### 布局原则
* 不到万不得已，不要写固定`width`和`height`
* 尽量用高级语法，如`calc``flex`
* 如果是`IE`，就全部写固定

#### `float`浮动布局（支持`IE8`）
	
	* 子元素加 float: left; 或 float: right;
	* 父元素加 .clearfix{content:’’; display: block; clear: both;}
	   	      .clearfix{zoom: 1;} //支持IE6
    
#### `flex`弹性布局（兼容`chorme``mobile`，不支持`IE8`）
    * 父元素加 display: flex
    * 父元素加 justify-content: space-between;


			   
#### 水平居中
`child`为不定宽`block`元素
	
	//方法一：转为 inline 元素
	child{display: inline;}
	parent{text-align: center;}
	
	//方法二：利用 table 长度自适应性，可将其看为定宽 block 元素
	child{display: table; margin-left/right: auto;}
	
	//方法三：margin 左右设同等值
	child{margin-left/right: 20px;}
	
	//方法四：translateX -50%
	child{position: absolute; left: 50%; transform: translateX(-50%);}
	parent{position: relative;}

`child`为定宽`block`元素

	child{width: 100px; margin-left/right: auto;}
	
`inline` `inline-block`元素以及图片

	parent{text-align: center;}
	
通用方法（`flex`布局）
	
	parent{display: flex; justify-content: center;}	
	
#### 垂直居中
`child`为定高/不定高`block`元素（`parent`高不确定）
	
	//方法一：translateY -50%
	child{position: absolute; top: 50%; transform: translateY(-50%);}
	parent{position: relative;}
	
	//方法二：利用 table (包括tbody、tr、td)标签。兼容IE。
	parent{vertical-align：middle;}
	
	//方法三：padding 上下设同等值
	child{padding-top/bottom: 20px;}

`child`为单行`inline`文本

	//方法一：height 和 line-height 设同等值
	parent{height: 40px; line-height: 40px;}
	
	//方法二：padding 上下设同等值
	parent{height: 40px; line-height: 20px; padding: 10px 0;}

`child`为多行`inline`文本以及图片

	//方法一：
	parent{display: table-cell; vertical-align: middle;}
	
	//方法二：padding 上下设同等值
	parent{height: 40px; line-height: 20px; padding: 10px 0;}

通用方法（`flex`布局）
	
	parent{display: flex; align-items: center;}

#### 左右布局

	//float + -margin（兼容 IE）
	父元素加.clearfix{content:’’; display: block; clear: both;}
	子元素分别加 float: left; 和 float: right; 
	
	//flex + -margin (可实现上下图片数量不一时的平均布局)  
	parent{display: flex; justify-content: space-between;}
	                                                                
#### 平均布局
￼`float`实现
<img src="https://i.loli.net/2018/01/04/5a4e1ddb9e90f.png
">

￼`flex`实现
<img src="https://i.loli.net/2018/01/04/5a4e1e4c26e7e.png
">

-------
参考：[写代码啦](https://xiedaimala.com/)




