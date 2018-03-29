---
title: Bootstrap 学习
date: 2018-03-29 18:17:04
categories:
tags:
---


#### `Bootstrap` 引入

[官网](https://v3.bootcss.com/getting-started/)下载

	* 生产环境：是指正式提供对外服务的。一般会关掉错误报告，打开错误日志。
	* 开发环境：程序员自己/公司用的。为了开发调试方便，一般打开全部错误报告。


---

#### 网格/栅栏系统

	* 默认内容都放在一个 .container 容器里。.container 默认水平居中。
	* row 默认左右 padding 为 15px。

```
<div class="container">
    <div class="row">
        <div class="col-md-2">.col-md-2</div>
        <div class="col-md-10">.col-md-10</div>
    </div>
    <div class="row">
        <div class="col-md-2">.col-md-2</div>
        <div class="col-md-9 col-md-offset-1">.col-md-9</div>
    </div>
</div>
```

---

#### 响应式怎么用

`Bootstrap` 有四个区间值。
	
	//<768px
	* @media (max-width: @screen-xs-max) { ... }
	
	//≥768px
	* @media (min-width: @screen-sm-min) and (max-width: @screen-sm-max) { ... }
	
	//≥992px
	* @media (min-width: @screen-md-min) and (max-width: @screen-md-max) { ... }
	
	//≥1200px
	* @media (min-width: @screen-lg-min) { ... }


---

#### `Bootstrap CSS` 组件怎么用



---

#### `Bootstrap jQuery` 组件怎么用





---