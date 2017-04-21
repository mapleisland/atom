---
title: Hexo 基本命令
categories:
- hexo

---

### 创建一个hexo博客
```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```
第一条命令会创建一个名为folder的目录,初始化完成后进入目录后安装npm依赖  
目录结构类似
```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

### 创建新文章

``` bash
$ hexo new "My New Post"
```
使用该命令系统会在`source/_posts/`下创建一个`My New Post.md`文件  
文件内容类似
```markdown
---
title: My New Post
date: 2017-04-17 16:37:34
tags:
---
```
其中title是日志标题,date是日志发布日期,tags是标签分类  
需要注意的一点是date的值和文件创建的时间必须为同一天,否则会显示不正确  
也可以自己在`source/_posts/`下创建一个新的`.md`文件,开始编辑新文章,hexo会自动识别  
查看更多: [Writing](https://hexo.io/docs/writing.html)

### 运行服务器

``` bash
$ hexo server
```

查看更多: [Server](https://hexo.io/docs/server.html)

### 生成静态文件

``` bash
$ hexo generate
```

查看更多: [Generating](https://hexo.io/docs/generating.html)

### 部署到服务器

``` bash
$ hexo deploy
```

查看更多: [Deployment](https://hexo.io/docs/deployment.html)
