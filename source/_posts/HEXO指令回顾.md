---
title: HEXO指令回顾
date: 2018-09-30 11:10:17
tags:
- HEXO
categories:
- HEXO
---

> 本文主要参考HEXO官方文档进行撰写，记录自己的建站过程，以供自己或他人在建站的作为简单参考。
> __HEXO官网地址__: _<https://hexo.io/>_

### 回顾
截止到本章节为止，已经使用了很多hexo指令了分别有：

- __init__
- __generate__
- __server__
- __clean__
- __new__
- __deploy__

这些指令基本上是hexo中比较常用的指令，本章会逐一介绍这些指令。

<!-- more -->

### init指令
```
hexo init [folder]
```
用于新建一个网站。如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。

### generate指令
```
hexo generate
```
也可简写为
```
hexo g
```
用于生成静态文件。静态文件存放在public文件夹下。

|选项|描述
|:------|:------|
|-d,--deploy|文件生成后立即部署网站
|-w, --watch|监视文件变动

### server指令
```
hexo server
```
也可简写为
```
hexo s
```
用于启动服务器。默认情况下，访问网址为：_<http://localhost:4000/>_。

|选项|描述
|:------|:------|
|-p, --port|重设端口
|-s, --static|只使用静态文件
|-l, --log|启动日记记录，使用覆盖记录格式

### clean指令
```
hexo clean
```
该指令没有简写。
用于清除缓存文件 (db.json) 和已生成的静态文件 (public)。
在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

### new指令
```
hexo new [layout] <title>
```
用于新建一篇文章。如果没有设置 layout 的话，默认使用 _config.yml 中的 default_layout 参数代替。如果标题包含空格的话，请使用引号括起来。

### deploy指令
```
hexo deploy
```
也可简写为
```
hexo d
```
用于部署网站。

|参数|描述
|:------|:------|
|-g, --generate|部署之前预先生成静态文件

### 其他
hexo 还有很多其他的指令，例如:
- __publish__
- __render__
- __migrate__
- __list__
- .
- .
- .

这里就不一一列举了，有兴趣的话可以自行查看官方文档:_<https://hexo.io/zh-cn/docs/commands>_。