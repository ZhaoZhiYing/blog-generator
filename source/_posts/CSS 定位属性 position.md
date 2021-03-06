---
title: CSS 定位属性 position
date: 2018-02-14 15:03:50
categories: CSS
tags:
---


> `position` 属性用于指定一个元素在文档中的定位方式。
> 
> 注意：`float`属性不可以和 `position` 属性共用。

##### `static`默认定位
默认值。没有定位，元素出现在正常的流中，此时`top` `bottom` `left` `right` `z-index` 无效。如果不用定位属性，那么这个`position`就不用设置。


##### `relative`相对定位
相对于以前的位置移动，偏移前的位置保留不动。不会脱离文档流。


##### `absolute`绝对定位

	* 相对于相对于最近的非 static 祖先元素定位移动，它会脱离文档流。
	* 当这样的祖先元素不存在时，则相对于 body 定位。
	* 当父元素被为 relative ，那 absolute 子元素将相对于其父元素定位。
	* 绝对定位的元素可以设置外边距，且不会与其他边距合并。


##### `fixed`固定定位
相对于浏览器窗口进行定位。元素的位置在屏幕滚动时不会改变。它会脱离文档流。应用于比如网页上的侧边栏和广告图。

一张图说清楚上面四种值的用法区别，如下：

<img src="https://i.loli.net/2018/02/14/5a83f972f1307.png
">

---

##### `inherit`继承定位
继承父元素的 `position` 值。如下图：

<img src="https://i.loli.net/2018/02/14/5a8429cb73349.png
">

上图中 `child` 继承了 `parent` 的 `position`，都是相对于浏览器窗口定位，所以 `top` `left` 取等值时候位置一致。

---

##### `sticky`粘性定位
粘性定位是相对定位 `relative` 和固定定位 `fixed` 的混合。元素在跨越特定阈值前为相对定位，之后为固定定位。粘性定位常用于页面滚动到一定程度时固定导航条的情况。

	p{ position: sticky; top: 10px; }
	
在 `viewport` 视口滚动到元素 `top < 10px` 之前，元素为相对定位。之后，元素将固定在与顶部距离 `10px` 的位置，直到 `viewport` 视口回滚到阈值以下。	

---