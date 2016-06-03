---
title: keystone
date: 2016-06-03 16:03:30
categories:
- install
tag:
- keystone
- express
- mongodb
- bootstrap
---
## keystone快速搭建简单项目
公司需要一个拥有管理页面的主页用来展示产品

{%link keystone http://keystonejs.com/%}快速搭建express、mongodb数据驱动的网站

安装过程就不赘述了,参考{%link getting-started http://keystonejs.com/getting-started/%}

重点讲下安装/使用过程中的坑

1.报Cannot find module 'unicode/category/So'

```bash
 # debian
$  sudo apt-get install unicode-data # optional
  # gentoo
$  sudo emerge unicode-data # optional

$  npm install unicode
```
2.虽然官网有强调,但这里当一个坑列出: 在执行以下命令之前要装{%link yeoman http://yeoman.io/%}

```bash
$ yo keystone
```
3.使用模板的concat页面提交数据时,server中断

其实就是调用了email功能，而安装模板没有带email-ak设置
修改 \models\Enquiry.js
{% codeblock %}
    Enquiry.schema.post('save', function() {
    	if (this.wasNew) {
    		this.sendNotificationEmail();
    	}
    });
{% endcodeblock %}

to

{% codeblock %}
    Enquiry.schema.post('save', function() {
    	if (this.wasNew) {
    		//this.sendNotificationEmail();
    	}
    });
{% endcodeblock %}

4.模板后台管理界面不能作修改
PS：可以hack入源码进行修改~~

附上最终修改效果:
{% asset_img amwares.jpg amwares%}
