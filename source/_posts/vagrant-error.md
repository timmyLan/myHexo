---
title: vagrant-error
date: 2016-05-23 11:37:42
categories:
- debug
tags:
- vagrant
---
## VM 无法访问

问题：

{% asset_img error.jpg error %}

出现原因：

安装homestead忘记将config.vm.box_version = settings["version"] ||= ">= 0.4.0"设置为>=0,导致VirtualBox重新下载。
强制关闭,导致VM重复无法访问。

解决办法：

将项目中的.vagrant 删除 并执行 vagrant up即可
