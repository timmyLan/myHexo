---
title: express+nginx
date: 2016-06-03 17:13:15
categories:
- express
tag:
- express
- nginx
- pm2
---
## nodejs 配合 nginx 部署

首先安装express并创建一个server

参考{%link 搭建express+mysql项目(一) http://timmylan.github.io/2016/04/25/express-mysql-1/%}

安装nginx
```bash
$ sudo add-apt-repository ppa:nginx/stable
```
如果 add-apt-repository 不可用
Ubuntu <=12.04.xx
```bash
$ sudo apt-get install python-software-properties
```
Ubuntu >12.04
```bash
$ sudo apt-get install software-properties-common
```
```bash
$ sudo apt-get update
$ sudo apt-get install nginx
```
配置nginx

删除default文件
```bash
$ sudo rm /etc/nginx/sites-enabled/default
```
新建一个example(自定义)文件
{% codeblock %}
server {
  server_name your.domain.com;
  listen 80;

  location / {
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_set_header X-NginX-Proxy true;
    proxy_pass http://127.0.0.1:3000;
    proxy_redirect off;
  }
}
{% endcodeblock %}

创建软连接
```bash
$ sudo ln -s /etc/nginx/sites-available/example /etc/nginx/sites-enabled
```
重启
```bash
$ sudo service nginx reload
```
配合pm2

安装{%link pm2 https://github.com/Unitech/pm2%}
```bash
$ npm install pm2 -g
```
用例:
```bash
$ pm2 start app.js
```