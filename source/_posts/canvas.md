---
title: canvas
date: 2018-02-11 00:04:54
tags:
---

#### 基本用法
* `canvas`负责在页面中设定一个区域，然后就可以通过`JS`动态地在这个区域中绘制图形。
* `canvas`默认是 `display: inline-block;`
* 要使用`canvas`元素，必须先设置`width` `height`属性，指定可以绘图的区域大小。

```
<canvas id="drawing" width="100" height="100">绘图区域</canvas>
```

* 要在这区域绘图，必须先取得绘图上下文，利用 `getContext()` 方法，如下：

```
var drawing = document.getElementById("drawing")
var context = drawing.getContext("2d")
```

* 使用 `toDataURL()` 方法，可导出图片。这个方法接收一个参数，即图片的格式，默认是`png`。如下：

```
//取得图片的 URL
var imgURL = drawing.toDataURL("image/jpg")

//显示图片
var img = document.createElement("img")
img.src = imgURL
document.body.appendChild(img)

//设置其他
img.download = '我的画'
img.target = '_blank'
...
```

---

#### 属性
##### 填充和描边

	strokeStyle 描边样式
	fillStyle 填充样式
	
	//用法
	context.strokeStyle = 'blue'
	context.fillStyle = 'red'
	
##### 绘制形状
	
	strokeRect(x, y, width, height) 边框坐标 
	fillRect(x, y, width, height) 填充坐标
	
	//绘制蓝色矩形
	context.fillStyle = 'blue'
	context.fillRect(10, 10, 50, 50)
	
	
##### 橡皮擦
	
	clearRect(x, y, width, height) 橡皮擦坐标
	
三者结合详细用法如下图：

<img src="https://i.loli.net/2018/02/13/5a827d0ede746.png
">

待完善...

---	