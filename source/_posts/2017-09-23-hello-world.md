---
title: Hello World
tags: hexo
date: 2017-09-23 23:24:40
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

<!-- more -->

### Create a Draft

#### 1、创建草稿

``` bash
$ hexo new draft "Title"
```

会在`source/_drafts`文件夹目录下面生成一个Title.md的文件。但是这个文件不被显示在页面上，链接也访问不到。也就是说如果你想把某一篇文章移除显示，又不舍得删除，可以把它移动到drafts目录之中。或者你还没有写好，可以把他理解为是新建一个草稿文件。

#### 2、预览草稿
``` bash
$ hexo s --drafts
```

会强行预览草稿。

#### 3、把草稿文章或页面变成文章
``` bash
$ hexo publish draft "Title"
```

将草稿文件移到`source/_posts`文件夹下面。发布命令格式：`hexo publish [layout] <filename>`，layout有三个值。`post`、`page`、`draft`。

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)