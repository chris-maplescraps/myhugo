+++
title = 'Hugo'
date = 2025-10-01T14:24:33+08:00
draft = false
slug = "3fadbfd"
description = ""
summary = ""
tags = [ "博客" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Hugo

这是一篇关于Hugo博客的技术文章，主要介绍Hugo的使用方法和配置

> [!NOTE]
> 知识点:
> - 博客根目录 指的是在博客文件夹内, 包含所有博客文章、配置文件、主题文件等
> - .yaml 和 .toml 都是配置文件格式, 用于配置博客的参数和外观, 推荐使用 .toml 格式, 因为它更简洁和易读

## 第一步
> [!IMPORTANT]
> 在还没开始配置Hugo之前，确保已经**安装**以下的软件:
> - [Go](https://go.dev/)
> - [Git](https://git-scm.com/downloads)

## 第二步
> **下载** 最新版本Hugo & Hugo主题:
> - [Hugo](https://gohugo.io/installation/windows/) ( 目前最新版本 >= v0.150.1 )
> - [Hugo 主题](https://themes.gohugo.io/) ( 本人使用hugo-narrow )

## 第三步
> - 选择你想要保存的路径, 点击右键 -> 选择Open Git Bash here,新建一个文件夹, 用于存放Hugo博客的文件
```git
mkdir C:\<blog_name>

example:
mkdir C:\hugo
```

> - 进入已经创建的文件夹
```git
cd C:\hugo
```

> - 初始化Hugo博客
```git
hugo new site .
```

> 下载 hugo-narrow 主题
```git
git submodule add https://github.com/hugo-narrow/hugo-narrow.git themes/hugo-narrow
```

> 配置 hugo-narrow 主题
```git
# 跳转到下载的hugo-narrow主题的exampleSite文件夹, 复制hugo.yaml文件到hugo_blog文件夹
C:\hugo\hugo_blog\themes\hugo-narrow\exampleSite
```

> - 编辑 `config.toml` 文件，配置Hugo博客的参数
> - 运行 `hugo server` 命令，启动Hugo博客的本地服务器
> - 打开浏览器，访问 `http://localhost:1313/` ，查看Hugo博客的效果

## 技术背景

简要介绍相关技术背景和问题场景...