---
title: CSS 移动端页面
date: 2017-12-13 16:07:34
categories: CSS
tags:
---
#### 先了解什么是响应式页面？
* 响应式页面就是随着设备属性（如宽高）的变化，网页也随着变化。

* 响应式页面需要两套图：手机端和网页端（推荐先做手机端）

------

#### 移动端如何做适配？ 
##### 1.`media query`媒体查询（响应式）

	<style> 
	@media(max-width:375px){ body{background: blue;} } 
	</style>
	//如果媒体满足max-width: 375px，就生效这个css样式

`@media`可以用`css`文件代替，在`link`里加上`media`查询条件,才能生效。
	
	<link rel=“stylesheet” href=“style.css” media=“(max-width: 320px)”>	
	
避免`css`层叠覆盖：
1.范围条件不要有交集。 
2.范围大的写在前面。  
	
------
   
##### 2.手机端加一个`meta`（响应式）
快捷写法：`meta:vp`

    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0"> 
    
    /*以下为注释*/
    device-width- 设备 viewport 的宽度
	initial-scale - 初始的缩放比例
	minimum-scale - 允许用户缩放到的最小比例
	maximum-scale - 允许用户缩放到的最大比例
	user-scalable - 用户是否可以手动缩放
     
加上上面`meta`后能做到在移动端`1:1`缩放，这样才是真正的适配移动端（设备多大页面多大，用户不能放大缩小）：

* 防止手机页面模拟`980px`宽度
* 防止页面在用户双击时候放大
* 防止页面变成横屏 

------

##### 3.方法一：使用`JS`动态调整`rem`
由于`rem`代表根元素（`html`元素）的 `font-size` 大小。那么可以先设置`1rem = html 的 font-size = 1page width`，这样后面就可以按比例直接调整`rem`。

	 <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
	 <script>
	     var pageWidth = window.innerWidth
	     document.write('<style>html{font-size:'+pageWidth/10+'px;}</style>') 
	 </script>
	 
	 // pageWidth/10 是将 rem 调整成整数，1rem = 0.1 html 的 font-size	 
 
`rem`可以与其他单位同时存在
	
	p{
		font-size: 16px;
		border: 1px solid red; //很小的单位上，可以用 px 或 em，比如线条。
		width: 0.5rem; 
	}
 
##### 方法二：在`scss`文件里添加，这个方法可实现`px`自动变`rem`

	@function px( $px ){
	  @return $px/$designWidth*10 + rem;
	}
	
	$designWidth : 750; // 750 是设计稿的宽度。 
	
	.child{
	  width: px(375);
	  height: px(160);
	  margin: px(40) px(40);
	  border: 1px solid red;
	  float: left;
	  font-size: 1.2em;
	}
	
----
参考：[写代码啦](https://xiedaimala.com/)





	
             
