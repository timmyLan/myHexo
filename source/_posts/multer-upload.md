---
title: multer实现文件上传
date: 2016-04-27 16:10:02
categories: express
---
## express利用multer中间件进行文件上传
因为小项目要用到上传文件功能,所以上网找到{% link multer https://github.com/expressjs/multer %}中间件实现该功能

1.第一步当然是安装multer
```bash
$ npm install multer
```
2.第二步配置中间件
```bash
$ vim app.js
```
{% codeblock lang:js %}
//...
var express = require('express')
var multer  = require('multer')

var app = express()
app.use(multer({
    dest: './uploads/'
}).single('file'));
//...
{% endcodeblock %}

3.添加form

xx.html
{% codeblock lang:html %}
<form action="/" method="post" enctype='multipart/form-data'>
  <table align="center">
      <tr>
          <td>myfile:</td>
          <td>
              <input type="file" name="file">
          </td>
      </tr>
  </table>
</form>
{% endcodeblock %}

4.配置路由

routes/xx.js
{% codeblock lang:js %}
router.post('/script/addFile',function(req,res,next){
    console.log('file',req.file)
});
{% endcodeblock %}

~~进阶
读取上传文件内容并写入数据库(这里直接读取内容写入数据库,其实思路应该记录路径用到的时候再读取,为研究到，有时间再研究)

{% codeblock lang:js %}
pool.getConnection(function(err, connection) {
    var script;
    var id = req.query.id;
    fs.readFile(req.file.path, function (err, data) {
        if (err) {
            return console.error(err);
        }
        script = data.toString();
        connection.query($sql.script.updateScript, [script,id], function(err, result) {
            if(result) {
                result = {
                    code: 200,
                    success:true
                };
            }
            // 以json形式，把操作结果返回给前台页面
            jsonWrite(res, result);

            // 释放连接
            connection.release();
        });
    });
});
{% endcodeblock %}

$sql.script.updateScript

{% codeblock lang:js %}
script:{
    updateScript:'update script set script=? where id=?'
}
{% endcodeblock %}

PS：这样直接写sql语句操作数据库太不友好了,应该用orm(Object relational mapper),google了下决定用sequelize。下一个blog就它了~~