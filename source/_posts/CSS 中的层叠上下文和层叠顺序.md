---
title: CSS 中的层叠上下文和层叠顺序
date: 2017-12-10 22:19:25
categories: CSS
tags:
---


#### 层叠顺序（由下往上）

	1.负 z-index（position）
	2.background
	3.border
	4.block
	5.float（ float/inline 在 float 上）
	6.inline/inline-block
	7.正 z-index（ position 元素由 z-index 大小决定层叠）

`z-index` 某些情况下可以影响层叠水平，但是只限于定位元素以及 `flex` 盒子的孩子元素；而层叠水平所有的元素都存在。	

---

#### 务必牢记的层叠准则
下面这两个是层叠领域的黄金准则。当元素发生层叠的时候，其覆盖关系遵循下面两个准则：

	1. 谁大谁上：当具有明显的层叠水平标示的时候，如识别的 z-indx 值，在同一个层叠上下文领域，层叠水平值大的那一个覆盖小的那一个。通俗讲就是官大的压死官小的。
	2. 后来居上：当元素的层叠水平一致、层叠顺序相同的时候，在 DOM 流中处于后面的元素会覆盖前面的元素。

备注：

	1.z-index:auto 所在的 <div> 元素是一个普通的元素，这时候 div 里的元素不受父级元素影响；
	2.当 z-index 一旦变成数值，哪怕是 0，都会创建一个层叠上下文，这时候父级元素决定子元素层级。'
	
---

#### 满足两个条件才能形成层叠上下文

	条件1：父级需要是 display:flex;或者 display:inline-flex;
	条件2：子元素的 z-index 不是 auto，必须是数值。
	
此时，这个子元素为层叠上下文元素，不是 `flex` 父级元素。

----

参考：

[写代码啦](https://xiedaimala.com/)  

[张鑫旭](http://www.zhangxinxu.com/wordpress/2016/01/understand-css-stacking-context-order-z-index/)