---
title: HEXO写作、主题及部署
date: 2018-09-28 18:47:56
tags:
- HEXO
categories:
- HEXO
---

> 本文主要参考HEXO官方文档进行撰写，记录自己的建站过程，以供自己或他人在建站的作为简单参考。
> __HEXO官网地址__: _<https://hexo.io/>_

### HEXO写作

可以通过执行__new__指令来创建博文。
```
hexo new [layout] <title>
```

#### 创建博文

尝试执行以下命令，访问博文地址观察下效果。
```
hexo new 我的第一篇博客
hexo clean
hexo generate
hexo server
```

<!-- more -->

{% asset_img firstblog.png %}

是可以明显看到刚刚所创建的那篇博文的。当然文章只有标题，没有实际内容，实际内容需要自己去编辑。编辑的话需要找到具体文件所在位置。执行__new__指令后是会打印出具体文件位置的，上面指令将会在__\_post__文件夹下自动生成一个__我的第一篇博客.md__的markdown文件，如下：

{% asset_img firstblogdir.png %}


#### 编辑博文
熟悉markdown语法的话编辑起来很简单，markdown语法就不做具体介绍，需要自己去学习。
可以尝试在文件中随便写点什么，然后刷新页面。编辑的内容是会立马生效的。

另外hexo提供了很多标签插件，详情可见:_<https://hexo.io/zh-cn/docs/tag-plugins>_。
标签插件有很多，并且官方文档中有详实的例子，这里就简单举个图片的例子，在文档中加入下面这段

```
{% img https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1538144411674&di=f3bab7ad765c8131bf9d18e9190b02db&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201603%2F17%2F20160317124201_jUnuR.jpeg [赤木晴子] %}
```

然后再刷新界面就能看到刚刚的那张图片了。

{% asset_img imgex.png %}

### HEXO主题

hexo可以自定义主题，当然也有丰富的开源主题供我们使用，可以在_<https://hexo.io/themes/>_去浏览并找到自己喜欢的主题。
下载自己喜欢的主题，然后放到__themes__文件夹内，然后修改站点配置中的__theme__配置即可。
例如下载好了next主题，然后再在站点配置中修改__theme__
```
#theme: landscape
theme: next
```

然后关闭HEXO服务，重新执行以下命令来启动HEXO服务。
```
hexo clean
hexo generate
hexo server
```
刷新界面，便可看到主题效果：

{% asset_img themeex.png %}

具体主题中的很多配置可以自行参考自己喜欢的主题的文档或是教程去自定义配置，每个主题都不尽相同。

### HEXO部署

#### 部署配置
部署之前必须先配置好站点配置中__deploy__相关信息：
```
deploy:
  type: // 类型
  repo: // 仓库地址
```
部署类型主要支持：Git、Heroku、Rsync、OpenShift、FTPSync，各类型的依赖需要自己安装。

#### 部署指令

部署指令很简单：
```
hexo deploy
```

#### github访问
部署到github的话，程序会尝试自动检测。
想要通过_https://<用户名>.github.io_来访问自己的博客的话，需要在自己账号下新增一个名称为__<用户名>.github.io__的代码仓库，然后通过配置__deploy__将博客部署至该仓库下：
```
deploy:
  type: git	// git类型
  repo: https://github.com/<用户名>/<用户名>.github.io.git // 注意最后有个.git不能少
  branch: master	// 必须在master分支下
  message: [message] // 这个自定义就好，可以不配置
```
另外需要修改站点配置中的__URL__：
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
#url: http://yoursite.com
url: https://github.com/<用户名>/<用户名>.github.io	// 将url修改为代码仓库地址、其他保持默认即可
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
```
最后执行__deploy__指令
```
hexo deploy
```
便可通过_https://<用户名>.github.io_来访问自己的博客啦。