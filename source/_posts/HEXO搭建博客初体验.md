---
title: HEXO搭建博客初体验
date: 2018-09-14 10:17:36
tags:
- HEXO
categories:
- HEXO
---

> 本文主要参考HEXO官方文档进行撰写，记录自己的建站过程，以供自己或他人在建站的作为简单参考。
> __HEXO官网地址__: _<https://hexo.io/>_

### HEXO的安装

#### 环境准备

安装HEXO前，必须确保安装机器上已经安装Git以及Node.js。如未安装，以下是对应的官网地址：
- __Git__: _<https://git-scm.com/>_
- __Node.js__: _<https://nodejs.org/>_

#### 安装HEXO

安装环境准备完毕后就可以直接通过npm来安装HEXO了：

```
npm install -g hexo-cli
```

<!-- more -->

### 建站

#### 初始化建站目录

HEXO安装完毕后，确定好建站目录，执行以下指令，自动初始化建站目录

```
hexo init <folder>
cd <folder>
npm install
```

执行完毕后，建站目录会自定生成HEXO的目录结构，如下：

```
.
├── _config.yml		// 站点配置文件
├── package.json	// 应用程序的信息
├── scaffolds		// 模板文件夹
├── source		// 资源文件夹
|   ├── _drafts		// 草稿
|   └── _posts		// 博文
└── themes		// 主题文件夹
```

在这通过注释的方式对各文件|文件夹进行了简单介绍，后续博文中会做进一步介绍。

#### 自动生成静态文件

建站目录初始化完成以后，再执行__generate__指令

```
hexo generate
```

自动生成博客所需的静态文件（HTML、JS、CSS等）

#### 启动服务

静态文件生成以后，最后执行__server__指令

```
hexo server
```

即可启动服务，通过<http://127.0.0.1:4000/>即可访问自己的博客，访问的效果图如下：

{% asset_img server-example.jpg %}



