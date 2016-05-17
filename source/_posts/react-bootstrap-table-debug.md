---
title: react-bootstrap-table server data
date: 2016-05-17 11:18:00
categories: debug
---

## react-bootstrap-table 插件缺少server data功能

{%link react-bootstrap-table https://github.com/AllenFang/react-bootstrap-table%} 插件作者短时间不打算添加server data功能
好在react-bootstrap-table有options data作为数据处理
解决方案：

引入react-paginate {%link react-paginate https://github.com/AdeleD/react-paginate%} 作为paginate

利用 options clickCallback回调方法请求相对数据

利用修改react-bootstrap-table的state(data),来控制显示数据
