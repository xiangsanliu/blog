---
title: Ubuntu16.04 LTS安装MySQL数据库并设置root用户允许远程连接
date: 2019-03-03 22:24:53
categories: 后端
tags: 
  - MySQL
  - 后端
  - Ubuntu
---

## 1. **SQL服务端** 

&emsp;&emsp;只需要一行命令：`apt-get install mysql-server`，安装过程中还需要设置root用户的密码
## 2. 更改root用户绑定的连接地址 

1. 登陆MySQL数据库：`mysql -u root -p `，输入刚刚设置的密码后登陆进数据库

2. 更新权限：`mysql> grant all privileges on *.* to 'root'@'%' identified by '*你的密码*' with grant option;`

3. 刷新权限：`mysql>flush privileges;`

## 3. 更改配置文件允许远程ip地址连接 

&emsp;&emsp;MySQL最新版中和远程ip地址连接有关的配置文件已经改到了`/etc/mysql/mysql.conf.d/mysqld.cnf`
所以输入命令：`sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`，找到这一段：

```
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address            = 127.0.0.1
#
# * Fine Tuning
```

注释掉这一行：`bind-address            = 127.0.0.1`，如下：

```
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
#bind-address           = 127.0.0.1
#
#* Fine Tuning
```

## 4. 最后，重启MySQL：`sudo service mysql restart`

