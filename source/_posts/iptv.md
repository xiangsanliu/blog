---
title: 浙江电信IPTV+上网 Padavan老毛子固件单线复用
date: 2020-01-13 16:50:41
tags:
---
# 浙江电信IPTV+上网 Padavan老毛子固件单线复用

## 前言

家里光猫离路由器太远了，路由器又只能放客厅才会能把WIFI信号辐射到每个角落，而客厅只有一个网口，只能想办法利用这个网口即上网又看IPTV。

<!--more-->

直接上网络拓扑图：

![网络拓扑图](https://cdn.jsdelivr.net/gh/xiangsanliu/images/img/007S8ZIlly1gj57ghvru9j30c904uwed.jpg)

## 1. 光猫设置

光猫型号是`TEWA-700G`，用管理员账号(获取管理员账号密码参考[获取TEWA-700G超级管理员密码改为自己路由拨号](https://jingyan.baidu.com/article/d169e186042e86436711d85d.html))登陆`http://192.168.1.1:8080`后，进入网络设置。

### 1.1 首先设置上网
我这里业务类型用的是路由和桥接混合模式，这个无所谓，能保证联通网络就行。LAN端口绑定全部。

![网络设置](https://cdn.jsdelivr.net/gh/xiangsanliu/images/img/007S8ZIlly1gj57gintbpj30ml0g1js1.jpg)

### 1.2 接着设置IPTV

记住`连接名称`43，一会儿要用，连接类型必须使用**桥接**，LAN端口绑定全部**不勾选**。

![IPTV设置](https://cdn.jsdelivr.net/gh/xiangsanliu/images/img/007S8ZIlly1gj57gjo87jj30m60dd0ta.jpg)

### 1.3 绑定VLAN

我这里eth0对应网口1，eth1对应IPTV，用户侧VLAN填1.2中记住的43，绑定WAN连接名称选择1.2中记住的`1_Other_B_VID_43`。

![VLAN](https://cdn.jsdelivr.net/gh/xiangsanliu/images/img/007S8ZIlly1gj57gk2pdgj30oe06qt8r.jpg)

光猫端设置完成。

## 2. 路由器设置

路由器型号是K2，已经刷了hiboy的老毛子固件。

### 2.1 外部网络(WAN)设置

拉到最后，按如图设置，STB端口可以自行选择，`VLAN LAN4`中填的是1.3 中设置的VLAN。

![wan](https://cdn.jsdelivr.net/gh/xiangsanliu/images/img/007S8ZIlly1gj57gkliwyj30yy0q5wg3.jpg)

### 2.2 内部网络(LAN)设置

转到IPTV设置，在`组播流量`中启用`启用 IGMP/MLD 侦听`，`M2U - 以太网交换机`选择`Multicast to Unicast`。

![LAN](https://cdn.jsdelivr.net/gh/xiangsanliu/images/img/007S8ZIlly1gj57gllouzj30qc0gmabf.jpg)

## 参考资料

1. [http://www.samllyangmao.com/thread-59696-1-1.html](http://www.samllyangmao.com/thread-59696-1-1.html)
2. [https://aisoa.cn/post-2220.html](https://aisoa.cn/post-2220.html)
3. [https://www.right.com.cn/forum/thread-347714-1-1.html](https://www.right.com.cn/forum/thread-347714-1-1.html)