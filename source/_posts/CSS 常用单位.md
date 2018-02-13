---
title: CSS 常用单位
date: 2018-02-09 17:31:23
tags:
---

### 字体大小

### `px`
像素`px`是相对于显示器屏幕分辨率而言的。

**12像素原则：**网页默认字体大小是`16px`，`Chorme`默认字体大小是 `12px`（比如如果设置是 `6px`，最小字号依然是 12px），`safari`没有最小字号。

**特点：**像素的大小是固定的。


### `em`

**特点：**1.`em`的值并不是固定的。2.`em`会继承父级元素的字体大小。

当定义`font-size`属性时，`1em`等于元素的父元素的字体大小。

如果没有设置文字大小，那它将等于浏览器默认文字大小`16px`。所以通`1em = 16px`，`2em = 32px`。

```
<div class="p1">
	<div class="p2">1</div>
  	<div class="p3">1</div>
</div>
```
	
```
.p1 {font-size: 16px; line-height: 32px;}
.P2 {font-size: 1em;}
.P3 {font-size: 2em; line-height: 2em;}

//P2{font-size: 16px; line-height: 32px} 
//P3{font-size: 32px; line-height: 64px}    
```

`em`相比`px`更加灵活，可用下面公式计算像素大小的等价 `em` 大小：

	em = 希望得到的像素大小 / 父元素字体像素大小

>`em` 可用于 `line-height` `font-size` `margin-bottom` `margin-top`

### `rem`
`rem`代表根元素（`html`元素）的 `font-size` 大小。当用在根元素的 `font-size` 上面时，它代表了它的初始值。

	html{font-size: 2rem} //32px

当用在非根元素的 `font-size` 上面时，相对于根元素字体大小。

	html{font-size: 1rem} // 此时 1rem = 1em = 16px
	p{font-size: 2rem} //32px


---

### 视口大小

### `vh`

视口高度，1vh=视口高度的1%


### `vw`

视口宽度，1vw=视口宽度的1%

---
