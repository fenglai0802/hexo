---
title: git子模块
date: 2016-09-17 15:31:17
tags:
	- git
	- 子模块
categories: git

---

# git子模块

### 问题

在开发项目A时，需要依赖项目B（实时更新）。同时希望A,B能够独立处理。

### 实际案例

举例来说，现在我参与的项目**网易有数（Youdata）**，它依赖了一个独立开发的图形库**NEV**，他们是并行开发的。如果只是简单的将**NEV**的代码copy到Youdata中，显然是有点傻逼，因为无法自动更新NEV的迭代。

### 处理方式

Git 通过子模块处理这个问题。子模块允许你将一个 Git仓库当作另外一个Git仓库的子目录。这允许你克隆另外一个仓库到你的项目中并且保持你的提交相对独立。

### 子模块相关操作：

#### 1.添加子模块 `$ git submodule add [url] [path]`

如

		$ git sub module add https://git.hz.netease.com/git/NEV/NEV.git src/webapp/res/nev

操作成功之后会生成一个.submodules的文件，其中记录了每个submodule的引用信息，知道在当前项目的位置以及仓库的所在。

#### 2.查看子模块 `$ git submodule`

如图

![](./images/git子模块/1.png)

ps: 如果子模块前面有一个-，说明子模块文件还未检入（空文件夹）

#### 3.初始化子模块： `$ git submodule init` --- 在首次检出仓库时运行一次

#### 4. 更新子模块：`$ git submodule update` 

这个命令才是最常用的，每次子模块更新或者切换分支了，就执行一次。

#### 5. 删除子模块：

* `$ git rm -cached [path]`
* 编辑`.gitmodules`文件，删除对应的子模块配置
* 编辑`.git/config`文件，删除对应的子模块配置
* 最后删除子模块的目录