---
title: babun与cmder
date: 2016-05-11 12:43:40
categories:
- install
tags:
- babun
- cmder
---
## babun配合cmder打造windows下的linux

1.下载 {% link babun http://babun.github.io/ %} && {% link cmder http://cmder.net/ %} 并安装

2.打开cmder,win+Alt+P打开设置界面 进入Startup > Tasks

3.添加一个task,命名为Babun

4.添加如下命令到Task Parameters
{%codeblock %}
/icon "%userprofile%\.babun\cygwin\bin\mintty.exe" /dir "%userprofile%"
{%endcodeblock%}

5.添加如下命令到Commands && save settings
{%codeblock %}
*%userprofile%\.babun\cygwin\bin\mintty.exe -o Transparency=0 /bin/env CHERE_INVOKING=1 /bin/zsh.exe
{%endcodeblock%}
效果如下图：
{% asset_img settings.jpg 新建 babun Tasks %}


