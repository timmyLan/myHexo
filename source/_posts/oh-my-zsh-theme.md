---
title: oh-my-zsh-theme
date: 2016-05-11 13:11:46
categories:
- config
tags:
- oh-my-zsh
---

## oh-my-zsh 主题配置
PS: oh-my-zsh{% link 主题 https://github.com/robbyrussell/oh-my-zsh/wiki/themes%}有很多,可以自行选择喜欢的进行配置

1.本人比较喜欢{% link Honukai主题 https://github.com/oskarkrawczyk/honukai-iterm-zsh%},进入github进行下载

2.进入下载目录honukai-iterm-zsh 输入如下命令

```bash
$ mv honukai.zsh-theme ~/.oh-my-zsh/themes/ #复制主题到~/.oh-my-zsh/themes/
```
3.修改.zshrc文件 => ZSH_THEME="honukai"
```bash
vim ~/.zshrc
```
4.重新加载~/.zshrc
```bash
source ~/.zshrc
```
效果如下:
{% asset_img theme.jpg oh-my-zsh 主题配置%}
