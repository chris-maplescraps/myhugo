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
|内容|**自定义模块、第三方模块、垂直行业模块 ** 存放所有您自己开发或从 Odoo App Store 下载的模块|**Odoo 官方核心模块** 存放 Odoo Community 和 Enterprise 版本提供的 **所有标准模块**（如 `base`、`web`、`sale`、`account` 等）|
|用途|**扩展** Odoo 功能。用于隔离您的自定义代码，<br />使其在 Odoo 升级时不受影响|**构成** Odoo 核心功能。是 Odoo 框架运行的基石，提供了所有基础模型和视图|
|修改|**鼓励修改和定制。** 这是您进行开发工作的地方|**强烈不建议修改。** 任何修改都会在 Odoo 升级时被覆盖，且可能导致系统不稳定|
|加载方式|必须通过 Odoo **配置文件**中的 `addons_path` 参数显式指定路径，Odoo 才能找到并加载它们|是 Odoo 源码中 **默认的加载路径之一**，无需配置即可加载|

---

### 开发 和 操作范围
✅ 核心观点：开发工作主要围绕 addons
在绝大多数情况下，您的 Odoo 开发工作确实只围绕着 addons（也就是您通过 addons_path 配置的外部自定义模块目录）进行。

**Odoo 架构设计的核心思想**：

- **安全隔离**： 将您的业务逻辑（自定义模块）与 Odoo 官方的内核和基础模块（核心 odoo/addons）完全分开。
- **可升级性**： 保证 Odoo 核心版本升级时（例如从 17.0 升级到 18.0），您只需关注自定义模块的兼容性，而无需担心修改的核心代码被覆盖。

### 1. 配置文件 ( odoo.conf )

这是您配置 Odoo 运行环境的关键文件。您需要修改它来：

- 指定数据库连接信息。
- 设置**`addons_path`** 来让 Odoo 找到您的自定义模块目录。
- 配置日志级别、端口号等。

### 2. 启动文件 ( odoo-bin )

这是 Odoo 服务器的启动脚本。虽然您通常不会修改它，但您会经常运行它来启动、停止或升级您的 Odoo 实例。

### 3. 核心模块（ 用于参考，而非修改 ）

当您需要**继承**或**扩展**一个核心模块（如 `sale` 或 `account`）的功能时，您需要查看位于 `odoo/odoo/addons` 目录中的源代码，以了解其类、字段和视图的定义。但您的实际修改代码仍会写在您**自己的外部模块**中。