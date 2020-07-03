---
title: N1小钢炮固件安装OpenWrt软路由
date: 2020-07-03 18:49:48
tags:
---

## 1. 下载镜像

`docker pull unifreq/openwrt-aarch64`

<!--more-->

## 2. 启动 OpenWrt

### 2.1 开启网卡混淆

`ip link set eth0 promisc on`

### 2.2 新建虚拟网卡

`docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 macnet`

其中`--subnet`参数后面跟的 IP 地址改成自己的网段，具体可以看电脑本机 IP 地址，如本机 IP 地址为`192.168.31.1`，那就改成`192.168.31.0/24`；
`--gateway`参数改成自己的路由器管理 IP 地址，如`192.168.31.1`

### 2.3 启动镜像

```shell
docker run -d \
    --name=OpenWrt \
    --restart always \
    --privileged \
    --network macnet \
    --ip 192.168.1.3 \
    unifreq/openwrt-aarch64:latest
```

其中`--ip`参数后的 IP 地址改为自己网段中任意一个与局域网内其它 IP 地址不冲突的 IP，如`192.168.31.3`

### 2.4 设置镜像 IP

#### 2.4.1 登陆 Portainer: `http://N1的IP:9000`

#### 2.4.2 左侧导航找到 `Containers`

#### 2.4.3 `Containers`找到`OpenWrt`点击`Quick Action`中最右边的按钮

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703190221.png)

输入命令：

```shell
vi /etc/config/network
```

按一下`i`键盘进入编辑模式，用键盘移动光标把`ipoaddr`后的 IP 地址改成 2.3 中设置的 IP 地址

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703190546.png)

改完后，按一下`ESC`，输入`:wq`，回车，完成

### 2.5 重启镜像

回到 2.4.2 中的页面，选中`OpenWrt`，点击`Restart`

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703190927.png)

## 3. 设置 OpenWrt

### 3.1 浏览器登陆 `http://2.3中设置的IP`, 默认密码`password`

### 3.2 点击 `网络 -> 接口`，在列表中第一个的 LAN 中点击修改

`基本设置`中的`IPV4网关`填如 2.2 中设置的 gateway

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703191554.png)

`DHCP服务器 -> 基本设置`中勾选`忽略此接口`

`DHCP服务器 -> IPv6 设置`中全部选择`已禁用`

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703191844.png)

点击`保存&应用`，OpenWrt 端设置完成~

## 4. 设置主路由器

以老毛子系统为例：`内部网络(LAN) -> DHCP服务器`，在`默认网关`中填入 2.3 中设置 的 IP，其它不动：

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703192050.png)

最后，手机或电脑重新 Wi-Fi。大功告成～
