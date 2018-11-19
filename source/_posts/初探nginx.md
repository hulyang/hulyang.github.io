---
title: 初探nginx
date: 2018-11-15 19:05:33
tags:
- java
- Nginx
- Linux
- Web
categories:
- Web
---

### Nginx 简介

#### Nginx 是什么

Nginx是一款轻量级的Web服务器、反向代理服务器及电子邮件（IMAP/POP3）代理服务器。其特点主要是占用内存小，并发能力强。

#### Nginx 可用来做什么

1. 处理静态资源
2. 反向代理
3. 负载均衡
4. 虚拟主机

#### 为什么要用 Nginx 

<!-- more -->

由于互联网行业的快速发展，对服务器并发能力的要求越来越高。传统Apache服务器，在高并发的情况下，需要消耗大量的内存，导致Http请求的平均响应速度降低。而Nginx采用C进行编写，选择了_epoll and kqueue_作为开发模型，能够支持高并发的同时，保持着非常低的CPU与内存占用率。所以，大势所趋，Nginx就火了起来。

### Nginx 的安装

#### Nginx 依赖

Nginx需要依赖以下三个类库：

- zlib	// gzip模块需要
- pcre	// rewrite模块需要
- openssl	// ssl功能需要

在Nginx安装之前要确保以上三个类库的正确安装

#### Nginx 下载与安装


Nginx的整个下载安装过程十分的简单、常规。
Nginx的安装包下载很简单，找到下载地址，直接_wget_下来就好：

```
wget http://nginx.org/download/nginx-1.12.2.tar.gz
```

然后就是解压安装包

```
tar -zxvf nginx-1.12.2.tar.gz
```

后面就是常规编译安装步骤

```
cd nginx-1.12.2
./configure
make
make install
```

这样整个安装就已经完成了。
安装好后的Nginx在 /usr/local/ 目录下
整个目录结构如下：

```
nginx/
|-- conf
|   |-- fastcgi.conf
|   |-- fastcgi.conf.default
|   |-- fastcgi_params
|   |-- fastcgi_params.default
|   |-- koi-utf
|   |-- koi-win
|   |-- mime.types
|   |-- mime.types.default
|   |-- nginx.conf
|   |-- nginx.conf.default
|   |-- scgi_params
|   |-- scgi_params.default
|   |-- uwsgi_params
|   |-- uwsgi_params.default
|   `-- win-utf
|-- html
|   |-- 50x.html
|   `-- index.html
|-- logs
`-- sbin
    `-- nginx
```

#### 安装验证

接下来可以来验证下安装是否成功：
```
cd /usr/local/nginx/sbin/
./nginx -t
```

当出现如下提示，则表示安装成功

```
nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful
```

#### Nginx 的启停


##### 启动
可以通过一下指令启动Nginx

```
./nginx
```

然后通过

```
ps -ef | grep nginx
```

查询Nginx进程，则可以看到有__master__和__work__两个进程，如下：

```
root      3660     1  0 20:24 ?        00:00:00 nginx: master process ./nginx
nobody    3661  3660  0 20:24 ?        00:00:00 nginx: worker process
root      3663  1118  0 20:24 pts/0    00:00:00 grep nginx
```

##### 关闭

关闭Nginx方式简单来说有两种

- 直接杀进程
- 结束命令

直接杀进程的话，要注意得先杀 __master__进程，再杀__work__进程：

```
kill 3660
kill 3661
```

结束命令有两种

```
./nginx -s stop	// 快速停止nginx
./nginx -s quit	// 完整有序的停止nginx
```
