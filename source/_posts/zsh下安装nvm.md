---
title: zsh下安装nvm
date: 2020-01-12 17:34:31
tags: 
  - node
---

# zsh下安装nvm

shell用的是zsh，在安装nvm的时候，显示安装成功但是在zsh下用不了，切换到bash倒是可以了。后来终于找到了一个插件[zsh-nvm](https://github.com/lukechilds/zsh-nvm)，可算解决了。

1. 首先下载插件`git clone https://github.com/lukechilds/zsh-nvm ~/.oh-my-zsh/custom/plugins/zsh-nvm`
2. 然后编辑`.zshrc`，在`plugins=(...)`下面添加一行`plugins+=(zsh-nvm)`
3. 再开个终端就完事儿了。