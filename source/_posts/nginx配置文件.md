---
title: nginx配置文件
date: 2018-12-12 09:26:31
tags:
- java
- Nginx
- Linux
- Web
categories:
- Web
---

<style>
table th:first-of-type {
    width: 20%;
}
</style>

nginx配置都在__conf/__目录下，本文中主要介绍配置文件__nginx.conf__。
查看配置文件内容，大体上如下：

```
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
	...
}
```

<!-- more -->

可以看出整个__nginx.conf__配置文件基本上可以分为以下三个部分：

- [全局配置](#全局配置)
- [event](#event)
- [http](#http)

接下来内容也会围绕这三部分展开。

### 全局配置

全局配置即直接写在__nginx.conf__配置文件最外层而不是被包在任何花括号内的配置信息。
这部分配置信息主要是设置一些影响Nginx服务器整体运行的配置指令。因此，这些指令的作用域是Nginx服务器全局。

默认配置文件中的全局配置内容基本如下：

```
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;
```

全局配置主要是配置了以下四个内容：

- [user](#user)
- [worker_processes](#worker-processes)
- [error_log](#error-log)
- [pid](#pid)

#### user

配置允许运行Nginx服务器用户（组）。

语法：

```
user <user> <group>
```

参数说明：

|参数|说明|默认值|
|:------|:------|:------|
|user|可以运行Nginx服务器的用户|nobody|
|group|可以运行Nginx服务器的用户组|nobody|

#### worker_processes

配置Nginx运行的work进程数。

语法：

```
worker_processes <number>
```

参数说明：

|参数|说明|默认值|
|:------|:------|:------|
|number|运行的work进程数量|1|

#### error_log

配置日志输出。

语法：

```
error_log <file> <level>
```

参数说明：

|参数|说明|默认值|
|:------|:------|:------|
|file|日志输出文件路径|logs/error.log|
|level|日志输出等级<br>常见日志等级有：[ debug &#124; info &#124; notice &#124; warn &#124; error &#124; crit &#124; alert &#124; emerg ]|error|

#### pid

配置进程pid存放路径。

语法：

```
error_log <file>
```

参数说明：

|参数|说明|默认值|
|:------|:------|:------|
|file|Nginx进程pid存放路径|logs/nginx.pid|

### event

__event__中的配置内容不多，示例如下：
```
event {
	use	epoll;
	worker_connections  1024;
}
```

其中主要配置了工作模式以及连接数上限。

__use__指定事件驱动模式，事件驱动模式有[ kqueue | rtsig | epoll | /dev/poll | select | poll ]。其中epoll模型是Linux 2.6以上版本内核中的高性能网络I/O模型，如果跑在FreeBSD上面，就用kqueue模型。

__worker_connections__指定每个work进程的最大连接数，所以整个Nginx可以接收的最大连接数 = work进程数 * 单个work的最大连接数。

### http

__http__用于配置http服务器。可以说是整个Nginx中最重要的部分。


