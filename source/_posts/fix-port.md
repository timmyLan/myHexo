---
title: 启动hexo遇到端口占用问题
date: 2016-04-25 11:20:19
categories:
- debug
tags:
- hexo
---
## 启动hexo,尝试打开localhost:4000,浏览器无响应
``` bash
$ hexo server
```
上网查了，发现是端口4000被占用。先解决问题，将端口号改为5000
``` bash
$ hexo server -p 5000
```

## 探究如何在windows找到端口状态
1.查看端口占用情况
``` bash
$ netstat -ano
```
2.查看指定端口的占用情况
``` bash
$ netstat -aon|findstr "4000"
```
{% asset_img netstatByPort.jpg 查看指定端口的占用情况%}
~~发现PID为5068的程序占用端口
3.查看PID对应的进程
``` bash
$ tasklist|findstr "5068"
```
{% asset_img tasklistByPID.jpg 查看PID对应的进程%}
4.把他干掉
```bash
$ taskkill /f /t /im FoxitProtect.exe
```
or
```bash
$ taskkill /f /pid 5068
```