---
title: Oracle数据库恢复与备份
date: 2020/7/14 19:24:00
---
### 登录Oracle  
	sqlplus /nolog
	conn /as sysdba
	//或
	sqlplus / as sysdba
### 恢复impdp
1. 在本地创建表空间
	> CREATE TABLESPACE NNC_DATA01(表空间名) DATAFILE 'E:\tablespace\nncdata01.dbf'(地址及bdf文件名) SIZE 1000M(表空间大小) AUTOEXTEND ON NEXT 50M(自动扩展空间大小) EXTENT MANAGEMENT LOCAL UNIFORM SIZE 256K;
2. 创建用户
	> create user yonghuming(设置用户名) identified by mima(设置密码) default tablespace NNC_DATA01(创建的表空间名) temporary tablespace temp;
3. 给用户授权：
	> grant connect,resource to yonghuming;  
	> grant create session to yonghuming;  
	> grant MANAGE SCHEDULER to yonghuming;  
	> grant CREATE VIEW to yonghuming;  
	> grant CREATE JOB to yonghuming;  
	> grant UNLIMITED TABLESPACE to yonghuming;  
	> grant dba to yonghuming;    //这个必须有  
4. 创建 导入数据库的存放目录，用于impdp，如果存在了就不用创建了。  
	> select * from dba_directories;  
	> create or replace directory dir as 'D:\importdir';  
4. cmd导入库数据泵  
	> impdp yonghuming(目标库用户名)/(目标库用户相应的密码)@orcl   DIRECTORY=importdir(地址目录变量)  dumpfile=OK051501BAK0628.DMP(需要导入的库文件)  remap_schema=OK051501(原库用户名):yonghuming(目标库用户名)  logfile=dtey20200628_dtey200706.log(日志文件名)  TABLE_EXISTS_ACTION=TRUNCATE;   
### 备份expdp
6. cmd导出数据库
	> //--先查询一下存放的路径   
	> select * from dba_directories;  
	> expdp okdemo(原用户名)/okmima(原用户密码)@orcl schemas=okdemo(原用户名) dumpfile=okdemobak0714.dmp(导出数据库文件名) logfile=okdemobak0714.log(日志文件名) directory=dir(数据库文件和日志文件存放地址变量);