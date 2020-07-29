---
date: 2020/7/14 22:52:00
---
1. 选择放置git仓库的文件夹，创建并初始化git本地仓库  
	> git init dev_work && cd dev_work  
2. 关联远端地址
	> git remote add -f origin https://github.com/xx/xx.git  
3. 开启git的 Sparse Checkout 模式（该模式专门用于git检出指定目录或文件，在config中配置）  
	> git config core.sparsecheckout true  
4. 设置需要拉取github上的文件目录
	> //这些目录写在了.git/info/sparse-check文件中。  
	> echo "source/posts(github上的目录或文件路径)" >> .git/info/sparse-check  
	> echo "css/fonts(可以写多个)" >> .git/info/sparse-check 
5. 从GitHub上拉取下来
	> git pull origin dev(对应分支名)   