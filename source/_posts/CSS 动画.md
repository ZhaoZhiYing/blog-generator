---
title: CSS 动画
date: 2018-02-13 01:43:03
categories: CSS
tags:
---

#### `@keyframes`关键帧
`@keyframes`指定一个`CSS`样式和动画将逐步从目前的样式更改为新的样式。 

	@keyframes myfirst{
	    0%{background: red;}
	    100%{background: yellow;}
	}
	
	//0% 和 100%  可以用 from 和 to 代替， 推荐使用 0% 和 100% 
	
#### `animation`动画

要使动画生效，需要将其绑定到一个选择器，且必须规定动画的名称和时长，这时需要使用`animation`。如下：
	
	div{
	    animation: myfirst 5s;
	}

属性

	* animation-delay 设置动画何时开始，以秒或毫秒计。默认是 0。
	
	* animation-direction 设置动画在每次运行完后是反向运行还是重新回到开始位置重复运行。默认是 "normal"。
		normal 正常播放。
		reverse 反向播放。
		alternate 动画在奇数次（1、3、5...）正向播放，在偶数次（2、4、6...）反向播放。
		alternate-reverse 动画在奇数次（1、3、5...）反向播放，在偶数次（2、4、6...）正向播放。
		initial 设置该属性为它的默认值。
		inherit 从父元素继承该属性。
		
	* animation-duration 设置动画一个周期的时长。默认是 0。
	
	* animation-iteration-count 设置动画重复次数，默认是 1。
		infinite 无限次重复动画。
		
	* animation-name 指定由 @keyframes 描述的关键帧名称。
		none 指定有没有动画。
		
	* animation-play-state 允许暂停和恢复动画。默认是 "running"。
		paused 指定暂停动画。
		running 指定正在运行的动画。
		
	* animation-timing-function 设置动画速度，即通过建立加速度曲线，设置动画在关键帧之间是如何变化。默认是 "ease"
		linear 动画从头到尾的速度是相同的。
		ease 动画以低速开始，然后加快，在结束前变慢。
		ease-in 动画以低速开始。
		ease-out 动画以低速结束。
		ease-in-out 动画以低速开始和结束。
		cubic-bezier(n,n,n,n) 在 cubic-bezier 函数中自己的值。可能的值是从 0 到 1 的数值。
		
	* animation-fill-mode 指定动画执行前后如何为目标元素应用样式。
		none 动画执行前后不改变任何样式。
		forwards 目标保持动画最后一帧的样式，最后一帧是哪个取决于animation-direction 和 animation-iteration-count。
		backwards 动画采用相应第一帧的样式，保持 animation-delay。
		both 动画将会执行 forwards 和 backwards 执行的动作。
		
---

#### `transition`过渡
* `transition`是指当它所绑定的属性发生改变的时候，根据速度曲线慢慢变化。比如`:hover` `:active` 或者通过`JS`实现的状态变化。
* `transition` 只对 `block` 元素生效。

属性

```
* transition-property 规定设置过渡效果的 CSS 属性的名称。
	none 没有属性会获得过渡效果。
	all 所有属性都将获得过渡效果。
	property 定义应用过渡效果的 CSS 属性名称列表，列表以逗号分隔。

* transition-duration 规定完成过渡效果需要多少秒或毫秒。 默认值是 0，意味着不会有效果。

* transition-timing-function 规定速度效果的速度曲线。
	linear 规定以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）。
	ease 规定慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier(0.25,0.1,0.25,1)）。
	ease-in 规定以慢速开始的过渡效果（等于 cubic-bezier(0.42,0,1,1)）。
	ease-out 规定以慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)）。
	ease-in-out 规定以慢速开始和结束的过渡效果（等于 cubic-bezier(0.42,0,0.58,1)）。
	cubic-bezier(n,n,n,n) 在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。

* transition-delay 定义过渡效果何时开始。以秒或毫秒计。
```

比如，将鼠标悬停在一个 `div` 元素上，逐步改变表格的宽度：
	
	div{ 
	transition-property: width; 
	} 
	
	div:hover{
		width: 300px;
	}

---

>使用时用容易将 `transform` 和 `transition`弄混，在此也记下`transform`的用法。

#### `transform`
`transform`是一个静态的属性。可以看作是与`width` `height`等同类的属性。应用于元素的2D 或 3D 转换。

	none 定义不进行转换。
	matrix(n,n,n,n,n,n) 定义 2D 转换，使用六个值的矩阵。
	matrix3d(n,n,n,n,n,n,n,n,n,n,n,n,n,n,n,n) 定义 3D 转换，使用 16 个值的 4x4 矩阵。
	translate(x,y) 定义 2D 转换。
	translate3d(x,y,z) 定义 3D 转换。
	translateX(x) 定义转换，只是用 X 轴的值。
	translateY(y) 定义转换，只是用 Y 轴的值。
	translateZ(z) 定义 3D 转换，只是用 Z 轴的值。
	scale(x,y) 定义 2D 缩放转换。
	scale3d(x,y,z) 定义 3D 缩放转换。
	scaleX(x) 通过设置 X 轴的值来定义缩放转换。
	scaleY(y) 通过设置 Y 轴的值来定义缩放转换。
	scaleZ(z) 通过设置 Z 轴的值来定义 3D 缩放转换。
	rotate(angle) 定义 2D 旋转，在参数中规定角度。
	rotate3d(x,y,z,angle) 定义 3D 旋转。
	rotateX(angle) 定义沿着 X 轴的 3D 旋转。
	rotateY(angle) 定义沿着 Y 轴的 3D 旋转。
	rotateZ(angle) 定义沿着 Z 轴的 3D 旋转。
	skew(x-angle,y-angle) 定义沿着 X 和 Y 轴的 2D 倾斜转换。
	skewX(angle) 定义沿着 X 轴的 2D 倾斜转换。
	skewY(angle) 定义沿着 Y 轴的 2D 倾斜转换。
	perspective(n) 为 3D 转换元素定义透视视图。


---

参考：[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Animations/Using_CSS_animations)	
