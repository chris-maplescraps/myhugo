+++
title = 'Odoo Knowledge'
date = 2025-11-19T16:02:13+08:00
draft = false
slug = "eb31fc9"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Odoo 项目解说

### Odoo 根目录结构
|| opt / odoo / addons| opt / odoo / odoo / addons|
| ---|---|---|
|特征| /opt/odoo/addons (外部/自定义 Addons) | /opt/odoo/odoo/addons (内部/核心 Addons)|
|位置|Odoo 安装目录的顶层，或位于您通过配置文件 $ADDONS_PATH 指定的任何路径|Odoo 源码目录内部，通常在 odoo/odoo/addons/|
|内容|**自定义模块、第三方模块、垂直行业模块 ** 存放所有您自己开发或从 Odoo App Store 下载的模块|**Odoo 官方核心模块** 存放 Odoo Community 和 Enterprise 版本提供的**所有标准模块**（如 `base`、`web`、`sale`、`account` 等）|
|用途|**扩展** Odoo 功能。用于隔离您的自定义代码，使其在 Odoo 升级时不受影响|**构成** Odoo 核心功能。是 Odoo 框架运行的基石，提供了所有基础模型和视图|
|修改|**鼓励修改和定制。** 这是您进行开发工作的地方|**强烈不建议修改。** 任何修改都会在 Odoo 升级时被覆盖，且可能导致系统不稳定|
|加载方式|必须通过 Odoo **配置文件**中的 `addons_path` 参数显式指定路径，Odoo 才能找到并加载它们|是 Odoo 源码中**默认的加载路径之一**，无需配置即可加载|