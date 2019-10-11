title: HEXO 迁移维护
date: 2016-12-28 13:06:53
tags: [hexo, node, git]
---
```
这个博客之前是用modernist主题来练手的，后来觉得好丑就没有继续更新了，今天偶然想起来还有这个
好东西，看看next的主题也很好，想着把它迁移过来，省的以后再丢失了
```

<!--more-->

### Github 两个库
#### 代码生成库  <font color="red">Eric--.github.io</font> (这个是 <font color="red">hexo d</font> 自动部署的)
* 目录结构
```
.
├── archives
│   ├── *
├── css
│   ├── *
├── fancybox
│   ├── *
├── images
│   ├── *
├── js
│   ├── *
├── lib
│   ├── *
├── tags
│   ├── *
├── index.html
└── CNAME
```
#### 源文件库 <font color="red">eric--.github.com</font>
* 目录结构
```
.
├── source
│   ├── *
├── _config.yml
└── package.json
```

---

### 本地文件库
#### <font color="red">hexo init</font> 生成的本地文件
* 目录结构
```
.
├── node_modules
│   ├── *
├── public
│   ├── *
├── scaffolds
│   ├── *
├── source
│   ├── *
├── themes
│   ├── *
├── _config.yml
└── package.json
```

---

### 维护
* 保证<font color="red">源文件库 eric--.github.com</font>最新状态
* 本地文件<font color="red">hexo d</font>后, 代码生成库更新到最新状态
* 重要的是维护好源文件库的三个文件<font color="red">source，_config.yml，package.json</font>
