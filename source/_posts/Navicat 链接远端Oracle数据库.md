---
date: 2020/7/13 13:43:00
---
Oracle官网下载Oracle的客户端 install client。  
官网地址：https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html

我下载的是：instantclient-basic-windows.x64-19.6.0.0.0dbru.zip

我解压到：D:\Oracle\instantclient_19_6

在这个目录下新建sqlnet.ora和tnsnames.ora两个文件  
sqlnet.ora文件内容  
　　SQLNET.AUTHENTICATION_SERVICES= (NTS)   
　　NAMES.DIRECTORY_PATH= (TNSNAMES, EZCONNECT)
tnsnames.ora文件内容  
　　orcl =   
　　　　(DESCRIPTION =      
 　　　　 (ADDRESS_LIST =         
   　　　　 (ADDRESS = (PROTOCOL = TCP)(HOST = ***192.168.146.143*** )(PORT = 1521))      
  　　　　　　)       
 　　　　　 (CONNECT_DATA =        
    　　　　　	(SERVICE_NAME = **orcl** )      
  　　　　　　)
　　　　　)  
　注：粗体部分需要按需配置，如果端口是自定义的也需要相应变更。

设置系统变量
1. 变量名：ORACLE_HOME  
变量值：D:\Oracle\instantclient_19_6  
2. 变量名：TNS_ADMIN  
变量值：D:\Oracle\instantclient_19_6  
3. 变量名：NLS_LANG  
变量值：SIMPlIFIED CHINESE_CHINA.ZHS16GBK  
4. 修改Path变量  
添加D:\Oracle\instantclient_19_6   
### 安装Nevicat
通过Tools（工具）->Options-> Miscellaneous -> OCI  将Nevicat的oci.dll更改为Oracle客户端的oci.dll


一切准备完成，可以直接用Nevicat链接远端Oracle数据库了。  
我看的是两个人不同操作，有的步骤可能多余，我也不想再仔细研究了

