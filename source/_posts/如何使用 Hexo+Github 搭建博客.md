---
title: 如何使用 Hexo+Github 搭建博客
date: 2017-10-09 22:25:20
categories: Git
tags:
---


### 准备工作
- `Node.js` 的安装和准备

- `git` 的安装和准备

- `gitHub` 账户的配置

- 了解基本的 `markdown` 语法

- 了解基本的命令行

接下来就可以进行后面的步骤，这里先检测下 `node` 和 `git` ，操作如下：

打开 `iTerm`（操作系统为`Mac`），执行以下命令，检测 `node` ，显示版本号则无误

	node -v

执行以下命令检测 `git` ，显示版本号则无误

	git version

### 安装Hexo
在自己认为合适的地方创建一个文件夹，打开 `iTerm` ，进入到该目录执行以下命令：

	npm install -g hexo-cli

这里也可以再验证是否安装成功，执行以下命令检测 `hexo` ，显示版本号则无误

	hexo -v

### 初始化博客
1.执行以下命令：

	hexo init blog

&nbsp;&nbsp;&nbsp;(`blog`是存放博客目录的文件夹，可自定义)

2.执行以下命令，进入 `blog`：
 
	cd blog

3.最后执行以下命令：
 
	npm i

### 配置博客
1.执行以下命令,会看到一个 `md` 文件的路径：

	hexo new 开博大吉

2.执行以下命令，会打开编辑器，编辑这个 md 文件，内容随意：

	start xxx.md

`macOS` 上对应的命令是 `open xxx.md`

3.执行以下命令：

	start _config.yml

`macOS` 上对应的命令是 `open _config.yml`

##### 这时会打开编辑器，按照下面顺序操作，编辑网站配置：

	1.把第 6 行的 title 改成你想要的名字
	2.把第 9 行的 author 改成你的大名
	3.把最后一行的 type 改成 type: git
	4.在最后一行，与type平齐，加上一行 repo: 仓库地址（请将仓库地址改为「你的用户名.github.io」对应的仓库地址）

##### 仓库地址以 `git@github.com:` 开头，获取步骤如下：

	1.在 GitHub 上新建一个空 repo ，repo 名称是「你的用户名.github.io 」（请将你的用户名替换成真正的用户名）
	2.创建后进入到一个页面，会看到仓库地址 SSH Keys（ git@github.com: 开头）
	3.回到 iTerm ，执行以下命令，安装 git 部署插件：

```
npm install hexo-deployer-git --save
```

4.执行以下命令，部署 `Hexo`:

```
hexo deploy
```

### 进入博客
	1.进入「你的用户名.github.io」对应的 repo
	2.进入Settings
	3.点击GitHub Pages的预览链接，就进入你的博客了！

### 主题设置
1.进入 [Themes版块](https://github.com/hexojs/hexo/wiki/Themes)，以 [https://github.com/litten/hexo-theme-yilia](https://github.com/litten/hexo-theme-yilia) 为例，点击进入主题 `GitHub` 首页。

2.依次执行以下命令行：

	cd ~/Desktop/myBlog

	cd themes
	
	git clone git@github.com:litten/hexo-theme-yilia.git
	
	cd ..
	
3.编辑 `_config.yml` ，将第 75 行改为：
	
	theme: hexo-theme-yilia	
	
4.依次执行完以下命令，刷新博客页面，会看到新的主题页面：

	hexo generate
	
	hexo deploy

#### 其他

	node_modules：是依赖包
	public：存放的是生成的页面
	scaffolds：命令生成文章等的模板
	source：用命令创建的各种文章
	themes：主题
	_config.yml：整个博客的配置
	db.json：source解析所得到的
	package.json：项目所需模块项目的配置信息

----

	
	
