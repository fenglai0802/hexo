---
title: Hexo + GitHub Pages 构建博客
date: 2016-08-03 12:54:27
tags:
---
## 1. 介绍篇

[DEMO](https://fenglai0802.github.io/)


#### 什么是Hexo

[Hexo](https://hexo.io/) 是一个简单地、轻量地、基于Node的一个静态博客框架，可以方便的生成静态网页。作者是台湾大学生tommy351。


#### 什么是GitHub Pages

[GitHub Pages](https://pages.github.com/) 可以被认为是用户编写的、托管在github上的静态网页。由于它的空间免费稳定， 可以用于介绍托管在github上的Project或者搭建网站。有两种形式: Project Site 和 User/Org Site。

GitHub Pages 生成的网站的默认域名是 username.github.io 或者 username.github.io/project-name ，但GitHub Pages是支持自定义域名的，参考教程：[github怎么绑定自己的域名](https://www.zhihu.com/question/31377141)


## 2. 安装篇

#### 安装中的一些小问题提醒

1. npm 报连接错误导致的安装失败：建议使用[淘宝NPM镜像](http://npm.taobao.org/)。
2. 权限错误：命令前加sudo

#### 环境

* 安装node (建议采用[n模块安装](https://fenglai0802.github.io/2016/08/03/%E5%88%A9%E7%94%A8%E6%A8%A1%E5%9D%97n%E7%AE%A1%E7%90%86node%E7%89%88%E6%9C%AC/))
* 安装git（安装Xcode自带）
* 申请github账号


#### 安装Hexo

1. 首先全局安装hexo

		$ npm install -g hexo


2. 创建工作文件夹，举例命名为`blog`;

3. 进入`blog`，初始化：

		$ hexo init

这里可能出现初始化错误，原因就是默认的npm出现连接错误，你需要手动执行`$ cnpm install`。
cnpm就是淘宝镜像的命令。

4. 安装server，用于本地调试：

        $ cnpm install hexo-server --save

如果不安装，现在的版本是不在带服务器的，导致后面执行`hexo server`报没有命令的错误。

5. 生成静态页面：

        $ hexo generate 或 $ hexo g

6. 启动本地服务，进行文章预览调试：

        $ $hexo server或 $ hexo s。

启动成功，根据提示在浏览器浏览器输入 http://localhost:4000 即可查看。


#### hexo一些常用命令(可以通过`hexo help`查看)：

* `hexo new "postName"` #新建文章

* `hexo new page "pageName"` #新建页面

* `hexo generate` #生成静态页面至public目录

* `hexo server` #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）

* `hexo deploy` #将.deploy目录部署到GitHub

* `hexo help` # 查看帮助

* `hexo version` #查看Hexo的版本

#### hexo关联配置Github

* 关联之前，你得先创建好自己的[GitHub Pages](https://pages.github.com/)，按着官方教程一步步来，或者自己google。

* 修改`blog`下的配置文件`_config.xml`:（repo的地址写你自己的GitHub Pages项目地址啊）

		deploy:

     		type: git

     		repo: https://github.com/fenglai0802/fenglai0802.github.io.git

    		branch: master

* 安装发布命令：

        $ cnpm install hexo-deployer-git --save

* 执行命名：

        $ hexo deploy

此时public文件夹下的内容就会被上传到你的github中fenglai0802.github.io的这个项目下。


* 然后再浏览器中输入 https://fenglai0802.github.io/ 就可以查看了。

* 每次部署的步骤，可按以下三步来进行。(建议自己写一个shell方便发布)

    	$ hexo clean

    	$ hexo generate

    	$ hexo deploy


## 3. hexo主题篇
