---
title: CSS 常见兼容性问题整理
date: 2018-05-09 11:25:58
categories: CSS
tags:
---

> 主要浏览器 Chrome Firefox Opera Safari ie8/9... 


##### 默认 `margin` `padding` 值

不同浏览器的默认 `margin` `padding`值不同。解决办法，初始化`CSS`的默认样式：

	*{margin: 0; padding: 0;}


##### `transform` 的兼容性写法	

以下是各浏览器 `CSS` 兼容前缀

	* -o-transform: rotate(7deg); // Opera
	* -ms-transform: rotate(7deg); // IE 9
	* -moz-transform: rotate(7deg); // Firefox 
	* -webkit-transform: rotate(7deg); // Safari 和 Chrome 
	* transform: rotate(7deg); // 统一标识语句


##### `!important`

`!important`对`IE`无效，对于一些差异问题，可以使用`!important`过滤`IE`


##### 被点击过后的超链接不再具有 `hover` `active` 属性

`CSS`正确书写顺序
	
	* :link //向未访问的链接添加特殊的样式。
	* :visited //设置访问过的页面链接的样式。
	* :hover //当有鼠标悬停在其上的链接样式。
	* :active //设置当你点击链接时的样式。

##### `ul` `ol` 列表缩进问题

清除 `ul` `ol` 列表缩进样式代码如下，此方法兼容 `IE`

	list-style:none;margin:0px;padding:0px; 


##### `font-family` 在不同浏览器显示差异问题

1.使用 `具体字体的名称 + 通用字体系列名` 方法来书写 `font-family`。浏览器会使用它可识别的第一个值。
	
	font-family: "Microsoft YaHei" sans-serif;
	
	//字体族大体上分为两类：sans-serif（无衬线体）和serif（衬线体）
	//一般非衬线字体在显示器中的显示效果会比较好

2.对于不同操作系统，默认的字体不同，这时可以直接写出多种字体（最后面也可以 + 通用字体系列名）。

	//中文
	font-family: "PingFang SC", "Hiragino Sans GB", "Heiti SC", "Microsoft YaHei", "WenQuanYi Micro Hei";
	
	//英文、数字
	font-family: Helvetica, Tahoma, Arial;
	
	//中英混合
	font-family: "Helvetica Neue", Helvetica, Arial, "PingFang SC", "Hiragino Sans GB", "Heiti SC", "Microsoft YaHei", "WenQuanYi Micro Hei", sans-serif;

	
3.一般字体文件都是用英文命名的，避免出现差异，最好中英文都写上。

	font-family: STXihei, "华文细黑", "Microsoft YaHei", "微软雅黑";

---
	