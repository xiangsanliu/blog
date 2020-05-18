---
title: windows终端改造记
date: 2019-05-13 14:59:45
tags: 
  - powershell
  - windows
---

## 1 前言

&emsp;&emsp;前段时间黑苹果出现问题，被迫转回windows 10，但是仍然对macOS的终端念念不忘，特别包管理工具，当然还有它的颜值，ys主题+onedark配色，简直美爆。

&emsp;&emsp;所幸，windows平台还有chocolatey和scoop两大包管理工具(当然，关于scoop是不是包管理工具，还有一些争议，这里就认为它是包管理工具吧)。但是windows的那个黑框cmd实在太丑了，而powershell的蓝框也是五十步笑百步。我又不想用第三方的终端，只好自己动手丰衣足食了。

<!--more-->

&emsp;&emsp;经过一番摸索，总算搞得还算能看了：

![效果图](https://i.loli.net/2019/05/13/5cd92e3dc7cbe33034.png)

## 2 包管理工具

&emsp;&emsp;chocolatey和scoop两个包管理工具我都使用过，网上对比的博文也有很多，就不展开说了。我选择的是scoop，原因只有一个，它不会申请管理员权限。它安装的软件存放路径是用户目录下的scoop文件夹，且不管装多少个软件，它往系统变量的path里只会添加一条记录(也就是不会污染path)。而chocolatey不仅需要管理员权限，还会把程序文件放得到处都是。

## 3 主题

&emsp;&emsp;一开始看了少数派的文章——[5 个 PowerShell 主题，让你的 Windows 终端更好看](https://sspai.com/post/52907)。文章里用的是[JanDeDobbeleer/oh-my-posh](https://github.com/JanDeDobbeleer/oh-my-posh)，但是翻了翻readme，没看到我想用的ys主题，项目中推荐的配色工具ColorTool也找到onedark配色，难道要我自己做？不存在的。

&emsp;&emsp;只能凑活用一下oh-my-posh了。

&emsp;&emsp;直到我某次翻scoop的文档时，看到了[lukesampson/pshazz](https://github.com/lukesampson/pshazz)，在这里找到了我心仪的ys主题。

&emsp;&emsp;主题列表在这里 [Theme-Screenshots](https://github.com/lukesampson/pshazz/wiki/Theme-Screenshots)，先放几个主题的效果图(图片来自lukesampson/pshazz)：

![ys](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200211204206.png)

![steeef](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200211204341.png)

### 3.1 使用主题

1. 安装 `scoop install pshazz'。

2. 使用 `pshazz use ${主题名}`，如`pshazz use ys`，这里的主题名可以通过`pshazz list`命令查看，参考主题列表的效果图选就是了。

3. 更多用法可通过`pshazz help`获取。

## 4 配色

&emsp;&emsp;找到pshazz后，我又顺藤摸瓜，找到了[lukesampson/concfg](https://github.com/lukesampson/concfg)。concfg是用于导入导出powershell配置文件的工具，所以当然也可以用来直接导入配色。仓库里没给效果图，我就给几张我试出来的吧。

- onedark

![onedark](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200211204409.png)

- pico

![pico](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200211204436.png)

- vs-code-dark-plus

![vs-code-dark-plus](https://xiangsanliu.oss-cn-hangzhou.aliyuncs.com/img/20200211204531.png)

### 4.1 使用配色

1. 安装concfg `scoop install concfg`。

2. 在使用前为保险起见，先备份一份`concfg export ${path}`，如`concfg export ~/concfg-backup.json`。

3. 使用 `concfg presets`查看已经预设的配色，`concfg import ${配色名}` 来使用，途中会要求两次确认。也可以通过import命令恢复备份或从网络/本地上导入配色。`concfg import <preset>|<path>|<url>`。

4. 更多用法可通过`concfg help`获取。