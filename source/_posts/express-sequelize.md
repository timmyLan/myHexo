---
title: 利用sequelize操作数据库
date: 2016-04-28 10:18:43
categories:
- express
tags:
- express
- orm
---
## express配合sequelize操作数据库
---解放直接操作数据库，从orm做起？？？

1.express直接用express-generator 生成

```bash
$  npm install express-generator -g
$  express -f --hbs
#这里生成了一个以handlebars为视图的空express项目
$ npm install
```

2.在目录上创建相应文件夹
```bash
#config 链接数据库
$ mkdir config && cd config && touch db.js
#models 模型
$ mkdir models
#routes(本来就有) 负责路由部分
```

3.安装sequelize&&mysql
```bash
$ npm install i --save sequelize
$ npm install i --save mysql
```

4.编辑db.js
{% codeblock lang:js %}
var Sequelize = require('sequelize');
module.exports = new Sequelize('test', 'root', null, {//密码为空用null或''表示
    host: 'localhost', // 数据库地址
    dialect: 'mysql', // 指定连接的数据库类型
    pool: {
        max: 5, // 连接池中最大连接数量
        min: 0, // 连接池中最小连接数量
        idle: 10000 // 如果一个线程 10 秒钟内没有被使用过的话，那么就释放线程
    }
});
{% endcodeblock %}

5.进入models新建user.js文件
{% codeblock lang:js %}
// user.js
var Sequelize = require('sequelize');
var sequelize = require('../config/db');
// 创建 model
var User = sequelize.define('user', {
    userName: {
        type: Sequelize.STRING // 指定值的类型
    },
    // 没有指定 field，表中键名称则与对象键名相同，为 email
    email: {
        type: Sequelize.STRING
    }
}, {
    // 如果为 true 则表的名称和 model 相同，即 user
    // 为 false MySQL创建的表名称会是复数 users
    // 如果指定的表名称本就是复数形式则不变
    freezeTableName: false
});

// 创建表
// User.sync() 会创建表并且返回一个Promise对象
// 如果 force = true 则会把存在的表（如果users表已存在）先销毁再创建表
// 默认情况下 forse = false
var user = User.sync({ force: false });

// 添加新用户
exports.addUser = function(userName, email) {
    // 向 user 表中插入数据
    return User.create({
        userName: userName,
        email: email
    });
};

// 通过用户名查找用户
exports.findByName = function(userName) {
    return User.findOne({ where: { userName: userName } });
};

//通过id找用户
exports.findById = function(id) {
    return User.findOne({ where: { id: id } });
};

{% endcodeblock %}

6.进入routes修改user.js文件
{% codeblock lang:js %}
var express = require('express');
var router = express.Router();
var user = require('../models/user');
/* GET users listing. */
router.get('/', function(req, res, next) {
    if(req.query.id){
        user.findById(req.query.id).then(function(user){
            res.send(user.userName);
        });
    }else{
      res.send('hello users');
    }
});
router.get('/addUser', function(req, res, next) {
    user.addUser('llan', 'llan@163.com').then(function() {
        // 查询新添加的用户
        return user.findByName('llan');
    }).then(function(user) {
        res.send(user.userName);
    });
});
module.exports = router;
{% endcodeblock %}

7.跑服务
```bash
$ npm start
```
8.看结果
浏览器输入{% link 127.0.0.1:3000 http://127.0.0.1:3000 %}
--->完美运行express示例界面(与前面做的无关系？？？)
{% asset_img express.jpg 示例 %}
浏览器输入{% link 127.0.0.1:3000/users http://127.0.0.1:3000/users %}
--->见到我们定义的hello users
{% asset_img users.jpg 自定义hello users %}
浏览器输入{% link 127.0.0.1:3000/users/addUser http://127.0.0.1:3000/users/addUser %}
--->界面出现llan(这货就是从数据库通过userName读出来的)
{% asset_img addUser.jpg 添加用户 %}
{% asset_img mysql.jpg mysql表 %}
浏览器输入{% link 127.0.0.1:3000/users?id=1 http://127.0.0.1:3000/users?id=1 %}
--->界面出现llan(通过id获取)
{% asset_img findById.jpg findById %}