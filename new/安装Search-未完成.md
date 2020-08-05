## hexo安装插件
1. 在 Git Bash Here 中输入
	> npm install hexo-generator-searchdb --save
2. 修改配置文件  
```` xml  
search:  
	path: search.xml  
	field: post  
	formate: html  
	limit: 10000  
````  
3. 修改主题的配置文件  
路径在：/themes/next下的_config.yml文件中。