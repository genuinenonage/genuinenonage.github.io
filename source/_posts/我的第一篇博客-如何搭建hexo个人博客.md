---
title: 如何搭建hexo个人博客
date: 2020/7/5 00:00:00
updated: 2020/7/29 23:12:00
comments: true
tags: 
- hexo
- next
categories: 
- [基础,hexo]
---
## 简要搭建hexo个人博客
* 首先电脑里要有Node.js(要选择安装upm)和git的应用程序。
接下来在cmd中操作即可。
* cmd中输入
    >npm install -g hexo-cli
* 安装hexo  
* 选择合适的博客存放文件夹，输入
    >hexo init blog 
* 等待初始化。
    >cd blog
    >hexo s
* 启动服务，可以在浏览器中看到个人博客，地址：localhost:4000/


### 常用命令
清理一下，清理缓存和已生成的静态文件
 > hexo clean

生成一下
 > hexo g  

启动一下
 > hexo s


### 部署到github
* 在github创建仓库，命名有强制要求：
	>//例如：nicheng.github.io  
    >你的昵称+  .github.io
* 更改_config.yml 文件
    >deploy:
    >>type: git   
	>>repo: 仓库地址  
    >>branch: master
* 部署到github上,cmd输入:
	>npm install --save hexo-deplover-git  
    >hexo d
* 输入昵称密码
* 部署成功，浏览器访问 你的昵称.github.io



### 卸载
* 卸载hexo  
	npm uninstall hexo-cli -g    
然后再文件夹中的blog，手动卸载。
注意：进行重装之前，如果还是在原来的位置上，必须手动清理了才能再次安装。






