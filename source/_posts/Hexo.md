---
title: 记一下第一次搭Hexo
date: 2018-09-11
tags:
- Hexo
- NexT
---

闲来无事，终于着手搭建自己的第一个博客了（其实很久前就想弄的，一直拖到现在...）。搜了一圈，还是Hexo简单点。第一篇就记一下搭建过程吧（其实是根本没想好有什么好写的）。
**分两篇，这一篇介绍下Hexo的搭建**

<!-- more -->

## 先丢两个官方文档
{% blockquote %}
    [Hexo](https://hexo.io/zh-cn/docs/)
    [NexT](http://theme-next.iissnan.com/getting-started.html)
{% endblockquote %}

## 前期准备

### 环境
- 前端嘛，都懂的，node和npm少不了，去[官网](https://nodejs.org/zh-cn/)下就可以了。如果你先npm安装`node_modules`包的时候太慢，可以用[cnpm](http://npm.taobao.org/)。
- `git`必备，[官网](https://git-scm.com/)，`Git bash`也是个好东西。

### github
1. 注册登录就不说了...在github新建一个`[你的github用户名].github.io`的项目，注意，一定要是你的github用户名，新建后，要过一段时间才能生效，可以直接访问https://[你的github用户名].github.io

## 开始搭建

### 安装
``` bash
$ npm install -g hexo-cli
```
或
``` bash
$ cnpm install -g hexo-cli
```

ps: 顺便说一句代码块的问题，比如我开启了代码块行号显示，但是某些代码块又不想显示行号，可以使用类似下面的写法，必须要用codeblock标签才行，用反引号好像不行，主要是`line_number:false`，这个官网文档上没有，我找了下源码才看到的：
```
{% codeblock line_number:false %}
alert('Hello World!');
{% endcodeblock %}
```

### 新建Hexo项目
进入一个硬盘区域，执行命令
```
$ hexo init <project name>
$ cd <project name>
$ npm install
```
第一个命令：初始化一个hexo项目，`<project name>`就是项目名称，可以自己取
第二个命令：进入刚初始化完成的项目文件夹
第三个命令：安装项目依赖

新建完成后，目录如下
{% codeblock line_number:false %}
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
{% endcodeblock %}

## 个性化配置
Hexo分为两种配置，一个是项目配置，对应项目根目录下的`_config.yml`文件；一个是主题配置，对应`themes/your_theme`下的`_config.yml`文件。这里先说说常用的项目配置。

### YMAL语法
首先简单了解下YAML的语法，如下，[参考](https://ansible-tran.readthedocs.io/en/latest/docs/YAMLSyntax.html)

{% codeblock lang:yaml line_number:false %}
favicon:
  small: /images/favicon-16x16-next.png
  #ms_browserconfig: /images/browserconfig.xml

keywords: "Hexo, NexT"

# Set rss to specific value if you have burned your feed already.
rss: false
{% endcodeblock %}

1. 大小写敏感 
2. 使用缩进表示层级关系 
3. 禁止使用tab缩进，只能使用空格键
4. 缩进长度没有限制，只要元素对齐就表示这些元素属于一个层级
5. 使用#表示注释 
6. 字符串可以不用引号标注
7. 冒号后面要加一个空格

### 常用配置
#### 网站相关配置
|参数|描述|
|---|---|
|title|网站标题|
|subtitle|网站副标题|
|description|网站描述，可用来SEO优化|
|keywords|网站关键词，可用来SEO优化|
|author|作者|
|language|网站语言|

#### 主题
```
theme: next # 默认landscape
```

#### 分页相关
```
per_page: 10 # 每页显示的文章量 (0 = 关闭分页功能)
```
#### 发布相关
{% codeblock lang:yaml line_number:false %}
deploy:
  type: git
  # 如果要用github.io做主页的话配置为 [你的github用户名].github.io的项目地址
  repository: https://github.com/xxx/xxx.github.io
  branch: master
{% endcodeblock %}

## 启动本地服务
{% codeblock lang:bash line_number:false %}
$ hexo server
{% endcodeblock %}
可简写为 `hexo s`，启动后浏览器中打开`http:localhost:4000`就可以看到页面了

## 发布
{% codeblock lang:bash line_number:false %}
$ hexo deploy
{% endcodeblock %}
可简写为 `hexo d`