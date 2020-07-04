---
title: N1小钢炮固件安装AdGuardHome
date: 2020-07-03 17:59:07
tags:
    - linux
---

# N1 小钢炮固件安装 AdGuardHome

## 一、安装

SSH 连接 N1，输入命令：

```shell
mkdir /opt/adguardhome
mkdir /opt/adguardhome/conf
mkdir /opt/adguardhome/work
docker run --name adguardhome -v /opt/adguardhome/work:/opt/adguardhome/work -v /opt/adguardhome/conf:/opt/adguardhome/conf --restart always --net host -d adguard/adguardhome:arm64-latest
```

<!--more-->

## 二、AdguardHome 配置

### 1. 浏览器打开 `http://N1的IP:3000`,输入账密码、端口等，dns 的端口填 80

### 2. 配置 DNS

![](https://cdn.jsdelivr.net/gh/xiangsanliu/images/20200703180900.png)

#### 2.1 上游 DNS 填入以下地址，并勾选并行请求：

```
tls://dns.quad9.net
tls://dns.google
tls://1.1.1.1
223.5.5.5
223.6.6.6
114.114.114.114
114.114.115.115
119.29.29.29
119.28.28.28
tls://1.0.0.1
```

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703181143.png)

#### 2.2 Bootstrap DNS 服务器填入：

```
114.114.114.114:53
8.8.8.8:53
8.8.4.4:53
1.1.1.1:53
208.67.220.220:53
208.67.222.222:53
2400:3200::1
```

#### 2.3 然后点击应用，并把`DNS 服务设定`中把`速度限制`改为 0

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703181330.png)

### 3. 配置广告过滤

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703181418.png)

先把自带的 3 个规则勾选上

![](https://cdn.jsdelivr.net/gh/xiangsanliu/images/20200703181506.png)

然后通过点击`添加阻止列表`来添加过滤规则，这里给出我的过滤规则。

```
My AdFilters
https://gitee.com/halflife/list/raw/master/ad.txt

xinggsf
https://gitee.com/xinggsf/Adblock-Rule/raw/master/rule.txt

大圣净化
https://raw.githubusercontent.com/jdlingyu/ad-wars/master/hosts

yhosts
https://raw.githubusercontent.com/VeleSila/yhosts/master/hosts

adgk手机去广告规则
https://gitee.com/banbendalao/adguard/raw/master/ADgk.txt

anti-ad
https://gitee.com/privacy-protection-tools/anti-ad/raw/master/easylist.txt

EasyList China
https://easylist-downloads.adblockplus.org/easylistchina.txt

EasyList
https://easylist-downloads.adblockplus.org/easylist.txt

googlehosts
https://scaffrey.coding.net/p/hosts/d/hosts/git/raw/master/hosts-files/hosts

1024_hosts
https://raw.githubusercontent.com/Goooler/1024_hosts/master/hosts

neoHosts
https://hosts.nfz.moe/full/hosts
```

## 三、路由器端设置

以老毛子系统为例：`内部网络(LAN) -> DHCP服务器`，在`DNS服务器 1`中填入 N1 的 IP，其它留空：

![](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703183149.png)

然后手机或电脑重新连接 Wi-Fi。

大功告成～

## 四、效果

![开启前](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703182655.png)

![开启后](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200703182910.png)
