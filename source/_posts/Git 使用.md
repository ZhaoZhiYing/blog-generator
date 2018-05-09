---
title: Git 使用
date: 2018-03-02 16:14:42
categories: Git
tags:
---

> 此博客仅为记录自己平常操作需要的一些命令


`Git` 是一个开源的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。

参考链接：
[猴子都能懂的 Git 入门](https://backlog.com/git-tutorial/cn/)  [Git - 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)

---

#### 配置 `git`

	git config --global user.name 你的英文名
	git config --global user.email 你的邮箱
	git config --global push.default matching
	git config --global core.quotepath false
	git config --global core.editor "vim"

---

#### 使用 `git` 有三种方式
1. 只在本地使用
2. 将本地仓库上传到 `GitHub`
3. 下载 `GitHub` 上的仓库

---

#### 查看本地 `git` 密钥

	ssh-keygen -t rsa -b 4096 -C "280273181@qq.com"
	
	cat ~/.ssh/id_rsa.pub

---

#### 删除本地 `git`

根目录下执行命令

	find . -name ".git" | xargs rm -Rf

---

#### 回退

##### 彻底回退到某个版本，本地源码同步回退

	git reset --hard <commit_id> 
	git push origin HEAD --force

<img src="https://i.loli.net/2018/03/02/5a9908ac019e4.png
">

##### 回退到某个版本，只保留源码

	git reset –-mixed <commit_id>
	
##### 只回退 `commit` 信息	

	git reset –-soft <commit_id>

---

#### 修改上次提交信息 `commit`

	git commit --amend 
	c //进入vim编辑
	:wq //保存退出
	git push

---
	
#### `hexo`博客每次更改后都执行以下命令：
	
	hexo generate //生成
	hexo deploy //部署		

---

#### `Git`常用命令速查表

<img src="https://i.loli.net/2018/03/02/5a9909fb4b8d1.jpg
">	

---


