+++
title = 'Python Tools'
date = 2025-11-04T16:16:27+08:00
draft = true
slug = "10bb50f"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Python Tools

## OpenCV
> 

## Certbot
##### :book: ​Cloudflare Configuration
在 Cloudflare 面板添加记录
:one: 登录 [Cloudflare 控制台](https://dash.cloudflare.com/login)
:two: 选择你的域名 `maplescraps.com`
:three: 在左侧菜单点击 **DNS -> Records**
:four: 点击 **Add record**
:five: 配置如下参数：

- Type: 选择 `TXT`
- Name: 输入 ` _acme-challenge`  (Cloudflare 会自动补全为 ` _acme-challenge.maplescraps.com`)
- Content: 粘贴 Certbot 终端里显示的那串长随机字符
- TTL: 保持 `Auto` 或选择 `1 min`

:six: 点击 **Save**