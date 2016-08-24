---
title: webpack-project
date: 2016-08-24 14:11:42
categories:
- webpack
tags:
- webpack
- bootstrap
---
## webpack-project
一个简单的webpack构建bootstrap自动化例子

github仓库
--------
{% link webpack-project https://github.com/timmyLan/webpack-project %}

目的
---------
* 希望通过该项目实现快速搭建bootstrap自动化开发环境
* 通过该项目熟悉webpack的使用方法
* 专注写业务流程,把重复的工作交给webpack完成，提高开发效率

注意
--------
请务必更新node.js (version>=5.x)

开始
-------
* 复制项目
```
$ git clone https://github.com/timmyLan/webpack-project.git
```
* 进入项目并安装包
```
$ cd webpack-project && npm install
```
* 全局安装rimraf(兼容linux,windows删除文件夹命令)
```
$ npm install rimraf -g
```
* 生产环境
```
$ npm run build
```
* 开发环境
```
$ npm start
```
环境说明
---------
* 生产环境
1.生成文件均放置到public目录
2.对文件进行混淆压缩

* 开发环境
1.运用热加载，自动刷新
2.添加sourceMap方便调试
