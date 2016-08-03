---
title: 利用模块n管理node版本
date: 2016-08-03 10:44:47
tags:
---
### 利用模块n管理node版本

* 由于node的版本迭代速度非常快，所以版本多样，所以升级版本或者切换版本都比较麻烦。本文介绍一下模块n的好处。

##### n

* n是node的一个模块，作者是TJ Holowaychuk（鼎鼎大名的Express框架作者），就像它的名字一样，它的理念就是简单：
> no subshells, no profile setup, no convoluted api, just simple

* 安装n

		$ sudo npm install -g n

* 安装完成之后，直接输入n后控制台就会输出当前已安装的node版本以及正在使用的版本（前面有个o的），通过上下方向键来选择想要使用的版本，回车生效。

		$ n
			0.10.1
		o   6.0.0

* 安装指定版本node

		$ n 6.0.0

* 安装最新版本node

		$ n latest

* 安装稳定版本node

		$ n stable

* 删除某个版本

		$ n rm 0.10.1

* 以指定的版本来执行脚本

		$ n use 0.10.21 some.js
