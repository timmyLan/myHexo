---
title: 安装mysql数据库
date: 2016-04-25 17:29:57
categories: express+mysql
---
## 安装数据库
1.{% link download http://dev.mysql.com/downloads/mysql/5.6.html %} zip文件,解压到D:\dev,重命名为mysql
2.配置MYSQL的环境变量
path 变量新增 ;D:\dev\mysql\bin
3.将my-default.ini另存为my.ini并修改为
{% codeblock %}
# The following options will be passed to all MySQL clients
[client]
#password   = your_password
port        = 3306

[mysql]
#设置mysql客户端的字符集
default-character-set = utf8

# The MySQL server
[mysqld]
port        = 3306
#设置mysql的安装目录
basedir = D:\dev\mysql
#设置mysql数据库的数据存放目录,必须是data或者\xxx-data
datadir = D:\dev\mysql\data
#设置服务器段的字符集
character_set_server = utf8
{% endcodeblock %}
4.注册服务
以管理员身份运行cmd
```bash
$ mysqld --install mysql5 --defaults-file=d:\dev\mysql\my.ini
```
5、启动服务
```bash
$ net start mysql5
```
6.登录MySQL服务器
```bash
$ mysql -h hostname -u username -p
```
-h选项：用于指定所希望连接的主机，即运行MySQL服务器的机器。如果在运行MySQL服务器的机器上运行该命令，则可以忽略该选项和hostname参数；如果不是，必须用运行MySQL服务器的主机名称来代替主机名称参数。
-u命令：用于指定连接数据库时使用的用户名称。
-p命令：用于指定用户输入的密码

7.安装navicat for mysql(又可以不用???)
{% link download http://www.ddooo.com/softdown/20238.htm %}
