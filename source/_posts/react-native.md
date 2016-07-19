---
title: react-native
date: 2016-07-19 15:54:30
categories:
- react
tags:
- react
- native
- Android
- Windows
---

react-native初次踩坑
===================================
有一段时间无写blog了，其实是我懒了:(
不对，是我遇到瓶颈了:)
发现用react写了个管理系统之后没有东西再创新了，缺少了一幅蓝图...
今日尝试搭建react-native,我要在手机端找到激情:)
——————————————————————————————————————————————————————————————我是吐槽完毕的分割线

直接参考官网{%link react-native getting-started http://reactnative.cn/docs/0.28/getting-started.html%}

与官网安装方式不同点
-------------------------------
1.我用的是babun控制台，安装python,node,git不用官网建议的chocolatey
安装python
```bash
#pact是babun的包管理器
$ pact install python-setuptools python-ming
$ pact install libxml2-devel libxslt-devel libyaml-devel
$ curl -skS https://bootstrap.pypa.io/get-pip.py | python
$ pip install virtualenv
$ curl -skS https://raw.githubusercontent.com/mitsuhiko/pipsi/master/get-pipsi.py | python
```

2.我只用过windows node,github 直接安装.exe

提升搭建速度的方法
-------------------------------
1.`react-native init AwesomeProject` 需要利用npm 安装包，所以在天朝会有一堵'隐形'的墙阻碍，可以改镜像地址
```bash
$ npm config set registry https://registry.npm.taobao.org
```
2.`react-native run-android` 需要下载{%link gradle-2.4-all.zip http://services.gradle.org/distributions/gradle-2.4-all.zip%}，这个不管是不是'天朝墙'的威力，这个包都有62.4M，用迅雷下快多了。下载完修改{YourProduct}\android\gradle\wrapper\gradle-wrapper.properties,将distributionUrl改为本地路径
```
distributionUrl=file:///E:/gradle-2.4-all.zip
```

跑官方例子遇到的坑
-------------------------------
```bash
#adb 无启动
Execution failed for task ':app:installDebug'.
> com.android.builder.testing.api.DeviceException: Timeout getting device list.
```
解决方法：
启动Genymotion->settings->ADB->Use custom Android SDK tools
{% asset_img settings.jpg settings%}

成功跑起官网例子
--------------------------------
{% asset_img finish.jpg finish%}

——————————————————————————————————————————————————————————————我是继续吐槽分割线

跑起了手机端的应用有那么一些激动:)，毕竟过去一年一直在web端跑程序，偶尔用chrome看手机端页面效果。现在这个是虚拟机的反馈，感觉很有新鲜感。
