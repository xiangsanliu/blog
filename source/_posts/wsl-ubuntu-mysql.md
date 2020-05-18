---
title: Ubuntu 18.04(WSL)下安装MySQL
date: 2020-02-11 20:02:10
categories: 后端
tags: 
  - MySQL
  - 后端
  - Ubuntu
---

# Ubuntu 18.04(WSL)下安装MySQL

## 前言

WSL ubuntu18.04下安装MySQL时碰到两个坑：

1. 安装后启动的时候出现目录权限的问题；
2. 因为安装的时候没有提示输入root密码，导致登陆不上等。

<!--more-->

## 一、安装

```
sudu apt install mysql-server
```

## 二、启动 (第一坑)

```
sudo service mysql start
```

启动时报错：`No directory, logging in with HOME=/`，目录权限问题。

解决方法是修改权限： 

```bash
sudo service mysql stop  #先停止服务

sudo usermod -d /var/lib/mysql/ mysql #修改目录权限

sudo service mysql start #启动MySQL
```

## 三、创建用户（第二坑）

输入 `mysql -u root -p` 提示输入密码，但是因为没有设置过密码，直接回车是登陆不进去的。只能用 `sudo mysql -u root -p` 登陆，提示输入密码时直接回车。

接下来新建一个不需要 `sudo` 权限的用户：

```sql
create user 'user'@'localhost' identified by 'password';

grant all on *.* to 'user'@'localhost';

FLUSH PRIVILEGES;
```

然后不用 `sudo` 权限也能用 `user` 用户登陆了：`mysql -u user -p`。

## 参考资料

1. [https://www.sunzhongwei.com/wsl-ubuntu-1804-installed-in-mysql-57](https://www.sunzhongwei.com/wsl-ubuntu-1804-installed-in-mysql-57)
2. [https://blog.csdn.net/weixin_43530726/article/details/91303898](https://blog.csdn.net/weixin_43530726/article/details/91303898)