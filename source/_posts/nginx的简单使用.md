---
title: nginx的简单使用
date: 2018-11-16 08:55:43
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

### 操作指令

#### 语法

```
nginx [-?hvVtTq] [-s signal] [-c filename] [-p prefix] [-g directives]
```

#### 选项

|选项|描述|
|:------|:------|
|-?,-h| 查看帮助信息|
|-v|显示版本信息|
|-V|显示版本信息和配置选项|
|-t|测试配置|
|-T|测试配置并转存|
|-q|测试配置时屏蔽非错误信息|
|-s signal|发送信号给master进程，信号有：stop（立即停止）、quit（优雅退出）、reopen（重启）、reload（重新加载配置）|
|-p prefix|设置文件路劲前缀(默认: /usr/local/nginx/)|
|-c filename|设置配置文件(默认: conf/nginx.conf)|
|-g directives|设置配置文件外的全局指令|

<!-- more -->
这里比较值得注意的，就是

```
./nginx -s reload
```
当我们修改配置文件后，不用关闭Nginx，直接执行上面那条指令，无需重启，就可以让配置文件生效，所以Nginx是支持热启动的。


### 常用功能

Nginx可以为我们提供一些常用的基础功能：

- 处理静态资源
- 反向代理
- 负载均衡
- 虚拟主机

下面来一一说明这些功能的简单配置：

#### 静态资源

配置访问静态资源很简单，只要通过__root__配置好静态资源根目录即可：

```
server {
	listen       80; # 服务监听的端口

	location / {
		root   html; # 静态资源根目录
	}
}
```

#### 反向代理

反向代理与静态资源类似，只要通过__proxy_pass__指定具体应用服务器即可：

```
server {
	listen       80;
	
	location / {
		proxy_pass   http://127.0.0.1:8080; # 应用服务器地址
	}
}
```

#### 负载均衡

负载均衡核心配置为__upstream__，然后通过反向代理去请求负载均衡服务：

```
# 负载均衡核心配置
upstream backend_server {
	server		127.0.0.1:8080;
	server		127.0.0.1:8081;
	server		127.0.0.1:8082;
}

server {
	listen		80;
	location / {
		proxy_pass	http://backend_server;
	}
}
```

#### 虚拟主机

所谓的虚拟主机，其实就是配置多个反向代理服务。使得实际一台机器却提供了多个应用服务的功能。在建站初期，网站访问量小，可以这么做，用于节省成本，但是一旦访问量增大，就不建议了。

```
server {
	listen		80;
	server_name	www.aaa.com;
	
	location / {
		proxy_pass		http://127.0.0.1:8080;
	}
}

server {
	listen		80;
	server_name	www.bbb.com;
	
	location / {
		proxy_pass		http://127.0.0.1:8081;
	}
}
```

#### Http服务

通过上面Nginx的几项基本功能的组合，便可以搭建出一个负载均衡的动静分离的HTTP服务，以下是一个简单示例：

```
upstream backend_server {
	server		127.0.0.1:8080;
	server		127.0.0.1:8081;
	server		127.0.0.1:8082;
}

server {
	listen		80;
	server_name	www.abc.com;
	
	location / {
		root		/home/com/abc;
	}
	
	location ~ \.(do|action)$ {
		proxy_pass	http://backend_server;
	}
}
```

Nginx的配置很灵活，很强大，如何去使用需要看具体的应用场景的需要。
Nginx暂时在工作中还没怎么用到过，希望日后能多去尝试，在使用中得到更好的理解和提高。