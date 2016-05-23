---
title: laravel
date: 2016-05-23 00:08:43
categories:
- install
tags:
- laravel
---
## 配置laravel环境
windows下模拟linux环境配置{%link laravel https://laravel.com/%}

1.安装{%link homestead https://laravel.com/docs/5.2/homestead%}，其实就是一个集合了laravel所需环境的虚拟机。
通过vagrant VirtualBox 来使用就可以了,直接参考{%link 官网 https://laravel.com/docs/5.2/homestead%}就行。
PS:国内的局域网太不靠谱了,安装的box还不能迅雷离线或者加速,share个福利{%link 百度云homestead http://pan.baidu.com/s/1gdF4gd9%}

2.Laravel 一键安装包{%link 下载 http://www.golaravel.com/download/%}
解压就用什么好说的~
解压到vagrant 配置的共享目录下改名为laravel

3.vagrant up

4.配置hosts 添加 192.168.10.10  homestead.app

5.网址输入http://homestead.app/

OK~demo如下
{% asset_img demo.jpg demo%}