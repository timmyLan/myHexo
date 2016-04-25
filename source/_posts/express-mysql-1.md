---
title: express+mysql+handlebar
date: 2016-04-25 16:36:06
categories: express+mysql
---
## 搭建express+mysql项目(一)
因为前段时间需要着手一个小工具开发,所以接触了{% link express http://expressjs.com/%}
。之前用express+mongodb+ejs,现在尝试用express+mysql+handlebar来实现该功能

1.首先安装express程序生成器
```bash
$ npm install express-generator -g
```
2.创建项目
```bash
$ express myapp --hbs
```
3.安装依赖
```bash
$ npm install
```
4.使用supervisor提高nodejs调试效率(可以不做???)
1、全局安装
```bash
$ npm install
```
2、修改packjson
{% codeblock lang:json %}
"scripts": {
    "start": "supervisor ./bin/www"
  }
{% endcodeblock %}
5.app.js中添加
{% codeblock lang:js %}
app.listen(3000, function () {
    console.log('my app listening on port 3000!');
});
{% endcodeblock %}
6.召唤hello world
```bash
$ npm start
```
7.浏览器中输入localhost:3000 观摩hello world
{% asset_img helloWorld.jpg demo%}
