---
title: Linux安装Mysql 8.0
date: 2020/08/27 10:42:00
tags: 
- 安装
categories:
- 安装
---
[https://blog.csdn.net/xiexinxx0225/article/details/107665316](https://blog.csdn.net/xiexinxx0225/article/details/107665316 "参考连接")  

## 卸载MariaDB  
MariaDB是Linux默认数据库，需先卸载。  
1. 使用 yum list installed | grep mariadb 检查MariaDB是否安装。
2. 使用 yum -y remove mariadb* 命令 卸载

## 删除MySQL对应的文件夹  
1. whereis mysql
2. find / -name musql

		[root@localhost /]# whereis mysql
		mysql: /usr/bin/mysql /usr/include/mysql
		[root@localhost lib]# find / -name mysql
		/data/mysql
		/data/mysql/mysql


3. 删除上两条命令查询出来的相关目录或文件。
	
		[root@localhost /]#  rm -rf /usr/bin/mysql /usr/include/mysql /data/mysql /data/mysql/mysql 

4. 重复输入1、2命令，是否删除完毕。

## 检查MySQL用户组和用户是否存在，如果没有，则创建

	[root@localhost /]# cat /etc/group | grep mysql
	[root@localhost /]# cat /etc/passwd |grep mysql
	[root@localhost /]# groupadd mysql
	[root@localhost /]# useradd -r -g mysql mysql
	[root@localhost /]#

## 命令下载Linux的Mysql安装包  

	[root@localhost ~]#  wget https://cdn.mysql.com/archives/mysql-8.0/mysql-8.0.19-linux-glibc2.12-x86_64.tar.xz

# 安装MySQL  
## 解压安装包  

	[root@localhost /]#  tar xvf mysql-8.0.19-linux-glibc2.12-x86_64.tar.xz
	[root@localhost /]# ls
	mysql-8.0.19-linux-glibc2.12-x86_64
	mysql-8.0.19-linux-glibc2.12-x86_64.tar.xz


## 操作  

1. 首先确保/usr/local/下没有mysql文件夹，如果有就删除  
2. 执行移动命令  
		
		[root@localhost ~]# mv mysql-8.0.19-linux-glibc2.12-x86_64 /usr/local/mysql


3. 在/usr/local/mysql目录下创建data目录  

		[root@localhost /]# mkdir /usr/local/mysql/data

4. 更改mysql目录下所有的目录及文件夹所属的用户组和用户，以及权限  

		
		[root@localhost /]# chown -R mysql:mysql /usr/local/mysql
		[root@localhost /]# chmod -R 755 /usr/local/mysql 

5. 下载链接库文件  

		[root@localhost bin]#  yum -y install libaio-devel.x86_64

6. 编译安装并初始化mysql,务必记住初始化输出日志末尾的密码（数据库管理员临时密码）  

		[root@localhost /]# cd /usr/local/mysql/bin
		[root@localhost bin]# ./mysqld --initialize --user=mysql --datadir=/usr/local/mysql/data --basedir=/usr/local/mysql

7. 编辑配置文件my.cnf，添加配置如下

		[root@localhost bin]#  vi /etc/my.cnf
 
		[mysqld]
		datadir=/usr/local/mysql/data
		port=3306
		sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
		symbolic-links=0
		max_connections=600
		innodb_file_per_table=1
		log-error=/usr/local/mysql/data/error.log

8. 测试启动mysql服务器

		[root@localhost /]# /usr/local/mysql/support-files/mysql.server start

9. 添加软连接，并重启mysql服务

		[root@localhost /]#  ln -s /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql 
		[root@localhost /]#  ln -s /usr/local/mysql/bin/mysql /usr/bin/mysql
		[root@localhost /]#  service mysql restart  

10. 登录mysql，修改密码(密码为步骤6生成的临时密码)

		[root@localhost /]#  mysql -u root -p
		Enter password:
		mysql>ALTER USER USER() IDENTIFIED BY 'yourpass';
		mysql>flush privileges;

11. 开放远程连接  

		mysql>use mysql;
		msyql>update user set user.Host='%' where user.User='root';
		mysql>flush privileges; 


12. 必须修改加密规则  

		1.输入 use mysql; 出现Database changed
		2.输入select user,host from user; 目的为了查看user的root 对应host是什么  我对应的是 %
		3.修改加密规则：输入ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';

		root:为数据库用户名
		123456：为数据库密码


13. 可以自由设置开机自动启动
		

		1、将服务文件拷贝到init.d下，并重命名为mysql
		[root@localhost /]# cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld
		2、赋予可执行权限
		[root@localhost /]# chmod +x /etc/init.d/mysqld
		3、添加服务
		[root@localhost /]# chkconfig --add mysqld
		4、显示服务列表
		[root@localhost /]# chkconfig --list




