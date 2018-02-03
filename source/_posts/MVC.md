---
title: MVC
date: 2018-02-02 22:32:28
tags:
---

#### `MVC` 是什么？
`MVC`（`Model View Controller` 模型-视图-控制）指一种代码组织形式。它将代码分成三层：

1. "视图层"（`View`），它是提供给用户的操作界面，是程序的外壳。
2. "数据层"（`Model`），也就是程序需要操作的数据或信息。
3. "控制层"（`Controller`），它负责根据用户从"视图层"输入的指令，选取"数据层"中的数据，然后对其进行相应的操作，产生最终结果。

#### `MVC` 三个对象分别有哪些重要属性和方法?
`View`
	
	 document.querySelector (获取对应的 html)
	
`Model`

	 init (初始化)
	 fetch (获取)
	 save (保存) 

`Controller`  

	 init (初始化 model 和 view)
	 loadMessages (加载数据)
	 bindEvents (绑定事件)
	 saveMessage (存储数据)