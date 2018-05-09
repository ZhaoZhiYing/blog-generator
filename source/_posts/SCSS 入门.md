---
title: SCSS 入门
date: 2018-04-16 17:00:45
categories: CSS
tags: 
---

#### `Sass` 和 `SCSS`

`SCSS` 是 `Sass 3` 引入新的语法，其语法完全兼容 `CSS3`，并且继承了 `Sass` 的强大功能。

	//Sass 转换为 SCSS
	$ sass-convert style.sass style.scss
	
	//SCSS 转换为 Sass
	$ sass-convert style.scss style.sass
	
`Sass`写法：不使用花括号和分号，通过缩排的方式表示选择符的嵌套层级，用换行符来分隔属性。
	
	#sidebar
	  width: 30%
	  background-color: #faa	
	  
`SCSS`写法：需要使用分号和花括号而不是换行和缩进。  

	#sidebar {
	  width: 30%;
	  background-color: #faa;
	}

---
	
#### `SCSS` 安装

依次执行以下命令行，进行全局安装。

	* npm config set registry https://registry.npm.taobao.org/
	* touch ~/.bashrc
	* echo 'export SASS_BINARY_SITE="https://npm.taobao.org/mirrors/node-sass"' >> ~/.bashrc
	* source ~/.bashrc
	* npm i -g node-sass

比如在桌面新建目录，进行使用。

	* mkdir ~/Desktop/scss-demo
	* cd ~/Desktop/scss-demo
	* mkdir scss css
	* touch scss/style.scss
	* open scss/style.scss

##### 将 `Sass` 编译成 `CSS`

多个编译

	//下面的命令表示将 sass 文件夹中所有 .scss (.sass)文件编译成 .css 文件，并且将这些 css 文件都放在 css 文件夹中。
	node-sass -wr scss -o css
	
单个编译
	
	node-sass <要编译的Sass文件路径>/style.scss <要输出CSS文件路径>/style.css
	
上面的命令在每次更改后都要执行一次，那么，能不能自动翻译？请执行以下命令。

	node-sass style.scss style.css -w style.scss	
---

#### `SCSS` 常用语法 - 嵌套

1.选择器嵌套

	div{
		border: 1px blue solid;
		h1{height: 16px;}
		span{width: 12px;}
	}
	
	//编译为
	div{border: 1px blue solid;}
	div > h1{height: 16px;}
	div > span{width: 12px;}

2.属性嵌套

	div{
	　　border: {color: red;}
     	font: {size: 12px;}
	}
	
	//编译为
	div{
	　　border-color: red;
     	font-size: 12px;
	}
	
3.引用父选择符：`&`
	
	a{
	  font-weight: bold;
	  &:hover{text-decoration: underline;}
	}	
	
	//编译为
	a{font-weight: bold;}
	a:hover{text-decoration: underline;}
	
---	






	
	