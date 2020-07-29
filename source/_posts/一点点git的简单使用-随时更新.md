---
date: 2020/7/15 19:16:00
---
#### 个性使用
1. 删除本地分支
	> git branch -d dev(分支名)  
2. 取消目录的git初始化  
	> rm -rf.git  
3. 克隆想要的分支到本地  
	> git clone --branch dev(分支名) https://github.com/xx/xx.git  


#### 基本使用
1. 初始化本地仓库  
	> git init git_work(仓库文件夹名称) && cd git_work  
2. 将变化提交到暂存区  
	> git add .  
3. 将本地暂存提交到版本库  
	> git commit -m "提交说明"  
4. 本地推送到远端分支  
	> git push origin dev(分支名)  
