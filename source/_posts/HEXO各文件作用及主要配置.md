---
title: HEXO各文件作用及主要配置
date: 2018-09-15 09:08:01
tags:
- HEXO
categories:
- HEXO
---

> 本文主要参考HEXO官方文档进行撰写，记录自己的建站过程，以供自己或他人在建站的作为简单参考。
> __HEXO官网地址__: _<https://hexo.io/>_

### HEXO文件目录

上篇博文中有提到HEXO文件目录结构如下：

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

接下来对各文件及目录进行进一步介绍。

<!-- more -->

#### _config.yml

站点配置文件，可以在此配置大部分的参数。具体配置中各参数会在后文中的站点配置中再做介绍。
#### package.json
应用程序的信息，EJS, Stylus 和 Markdown renderer 已默认安装，可以自由移除。此部分信息不建议修改。
```
package.json
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": ""
  },
  "dependencies": {	// 依赖信息
    "hexo": "^3.0.0",
    "hexo-generator-archive": "^0.1.0",
    "hexo-generator-category": "^0.1.0",
    "hexo-generator-index": "^0.1.0",
    "hexo-generator-tag": "^0.1.0",
    "hexo-renderer-ejs": "^0.1.0",		// EJS
    "hexo-renderer-stylus": "^0.2.0",		// Stylus
    "hexo-renderer-marked": "^0.2.4",		// Markdown
    "hexo-server": "^0.1.2"
  }
}
```
#### scaffolds

模版文件夹。新建文章时，Hexo会根据scaffold来建立文件。
文件夹内有以下三个模板：
```
draft.md	// 创建草稿的模板
page.md		// 创建新页面的模板
post.md		// 创建新博文的模板
```
创建文件时，模板中的Front-matter内容会自动填充到对应文件中。
#### source

资源文件夹，是存放用户资源的地方。
除\_posts文件夹之外，开头命名为\_ (下划线)的文件/文件夹和隐藏的文件将会被忽略。Markdown和HTML文件会被解析并放到public文件夹，而其他文件会被拷贝过去。
暂时查看source文件夹下只有\_post文件夹，是因为HEXO初始化时自动生成了一篇hello-world.md。
具体如何创建新的博文、草稿、以及新的界面会在后续博文中再做介绍。

#### themes

主题文件夹，HEXO会根据主题来生成静态文件，默认主题为landscape。

### 站点配置

上文中已经有过介绍：_config.yml 为站点配置文件。可以在_config.yml中进行大部分的配置。

#### 网站
|参数|描述|
|:------|:------|
|title|网站标题|
|subtitle|网站副标题|
|description|网站描述|
|keywords|关键词（暂时没发现有什么用处）|
|author|作者名称|
|language|网站使用的语言（一般搭配主题中的语言来设置）|
|timezone|网站时区。Hexo 默认使用您电脑的时区。时区列表。|

> 这部分即网站的一些定制信息，需要自己根据自身需求去完善。

#### 网址
|参数|描述|默认值|
|:------|:------|:------|
|url|网址网址||
|root|网址根目录|/|
|permalink|文章的永久链接格式|:year/:month/:day/:title/|
|permalink_defaults|永久链接中各部分的默认值| ||

> 这部分主要为网址路劲配置，主要修改URL即可。

#### 目录
|参数|描述|默认值|
|:------|:------|:------|
|source_dir|资源文件夹，这个文件夹用来存放内容|source|
|public_dir|公共文件夹，这个文件夹用来存放生成的站点文件|public|
|tag_dir|标签文件夹|tags|
|archive_dir|归档文件夹|archives|
|category_dir|分类文件夹|categories|
|code_dir|Include code 文件夹|downloads/code|
|i18n_dir|国际化（i18n）文件夹| :lang|
|skip_render|跳过指定文件的渲染您可使用_glob表达式_来匹配路径。|||

> 这部分为HEXO自动生成文件后的目录情况，基本不需要做任何修改，保持默认值即可。

#### 文章
|参数|描述|默认值|
|:------|:------|:------|
|new_post_name|新文章的文件名称|:title.md|
|default_layout|预设布局|post|
|auto_spacing|在中文和英文之间加入空格|false|
|titlecase|把标题转换为title case|false|
|external_link|在新标签中打开链接|true|
|filename_case|把文件名称转换为(1)小写或(2)大写|0| 
|render_drafts|显示草稿|false|
|post_asset_folder|启动Asset文件夹|false|
|relative_link|把链接改为与根目录的相对位址|false|
|future|显示未来的文章|true|
|highlight|代码块的设置|||

> 这部分主要对博文中的部分信息进行配置，基本不需要做任何修改，保持默认即可。

#### 分类 & 标签
|参数|描述|默认值|
|:------|:------|:------|
|default_category|默认分类|uncategorized|
|category_map|分类别名||
|tag_map|标签别名|||

> category_map以及tag_map配置为名称-路径的这种K-V形式，以category_map最为示例：
> category_map:
> &nbsp;&nbsp;&nbsp;&nbsp;分类1:category1
> &nbsp;&nbsp;&nbsp;&nbsp;分类2:category2

#### 日期 / 时间格式
|参数|描述|默认值|
|:------|:------|:------|
|date_format|日期格式|YYYY-MM-DD|
|time_format|时间格式|H:mm:ss|

> Hexo使用Moment.js来解析和显示时间。这部分基本上不需要修改，保持默认即可。

#### 分页
|参数|描述|默认值|
|:------|:------|:------|
|per_page|每页显示的文章量(0 = 关闭分页功能)|10|
|pagination_dir|分页目录|page|

> 这部分很好理解，根据个人喜好进行配置就好。

#### 扩展
|参数|描述|
|:--|:------|
|theme|当前主题名称。值为false时禁用主题|
|deploy|部署部分的设置|

> 主题和部署会在后续博文中再做介绍。

### 自定义博客

已经大致了解过站点的相关配置，接下来简单修改下配置，看看效果。

#### 修改配置
简单修改_config.yml中的关于网站部分的配置，修改如下：
```
title: hulyang
subtitle: hulyang's blog
description: hulyang blog desc 
keywords:
author: hulyang
language:
timezone:
```

#### 启动服务
配置修改并保存成功以后，执行以下指令，启动服务：
```
hexo clean	// 清除缓存文件 (db.json) 和已生成的静态文件 (public)。
hexo generate	// 自动生成静态文件
hexo server	//启动服务
```
统一访问_<http://127.0.0.1:4000>_来看看效果如何：
{% asset_img example.jpg %}

> 配置生效，标题等与刚刚的配置相符