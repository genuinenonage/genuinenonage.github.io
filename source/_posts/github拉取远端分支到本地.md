---
date: 2020/7/19 19:38:00
---
## github 拉取远端分支到本地
1. 新建一个文件夹
2. 初始化，在 git base 中输入
	>git init
3. 与远端master建立链接
	>git remote add origin 仓库链接地址https://github.com/xx/xx.git  
	>//如果第一遍输入错误，可以输入 git remode rm origin ，删除上一步的操作之后重新输入  
4. 把远程分支拉到本地
	>git fetch origin dev(dev为远程仓库的分支名)
5. 切换到分支
	>git checkout dev(dev为远程仓库的分支名)
6. 以后每次使用时最好先：把分支的最新内容拉取到本地
	>git pull origin dev(远程分支名)