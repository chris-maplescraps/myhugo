+++
title = 'Odoo Deployment'
date = 2025-11-18T11:04:43+08:00
draft = false
slug = "bcb86a1"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Odoo Deployment

- odoo.conf 配置管理文件，管理员密码，数据库保存路径，日志保存等等
- odoo 下载 [odoo github official](https://github.com/odoo/odoo.git)
- pgadmin4 用于管理数据库
- 安装 odoo 依赖项，建议指定python版本进行安装 requirements.txt
  - pip3.10 install -r requirements.txt

## 部署 Odoo 前提条件
#### 1. 安装 node.js
> **准备工作**
>
> ```bash
> sudo apt update
> sudo apt install -u curl ca-certificates build-essential gss g++ make
> ```
> **开始安装**
> ```bash
> curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
> 
> # 使当前 Shell 会话加载 nvm（如使用 zsh，请改为 ~/.zshrc）
> export NVM_DIR="$HOME/.nvm"
> [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
> [ -s "$NVM_DIR/bash_completion" ] && . "$NVM_DIR/bash_completion"
> ```
> **安装与切换 Node 版本**
> 
> ```bash
> # 安装最新 LTS（截至 2025 年推荐 Node 22 LTS）
> nvm install --lts
> 
> # 或安装指定版本（示例：22.x）
> nvm install 22
> 
> # 切换当前会话使用的版本
> nvm use 22
> 
> # 设置默认版本（新终端自动使用）
> nvm alias default 22
> ```
>
#### 2. 安装 git
> **方法一：使用系统 APT 仓库安装 Git（推荐）**
> 
> ```bash
> sudo apt update
> sudo apt install -y git
> 
> # 验证
> git --version
> which git    # 通常为 /usr/bin/git
> ```
> 
> **方法二：使用 Git 官方 PPA 安装最新版本（推荐）**
> 
> ```bash
> sudo apt update
> sudo apt install -y software-properties-common ca-certificates
> 
> # 添加官方 PPA 仓库
> sudo add-apt-repository -y ppa:git-core/ppa
> 
> # 更新并安装
> sudo apt update
> sudo apt install -y git
> 
> # 验证
> git --version
> ```
> 

## Step 1: 安装 Odoo 依赖项
> ```bash
> sudo apt update
> sudo apt install git python3-pip build-essential wget python3-dev > python3-venv \
>     python3-wheel libfreetype6-dev libxml2-dev libzip-dev libldap2-dev > libsasl2-dev \
>     python3-setuptools node-less libjpeg-dev zlib1g-dev libpq-dev \
>     libxslt1-dev libldap2-dev libtiff5-dev libjpeg8-dev libopenjp2-7-> dev \
>     liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev libxcb1-dev
> ```

## Step 2: 创建系统用户
> ```bash
> sudo useradd -m -d /opt/odoo15 -U -r -s /bin/bash odoo15
> ```
> |部分|含义|解释|
> |---|---|---|
> |sudo|提升权限|以超级用户（root）身份执行后续命令|
> |useradd|	用户添加命令|	这是用于创建新用户的命令|
> |-m|	创建主目录|	如果主目录不存在，则创建它|
> |-d /opt/odoo15|	指定主目录|	将新用户的主目录设置为 /opt/odoo15。这是安装 Odoo 文件的常用位置|
> |-U|	创建同名用户组|	创建一个与用户名（odoo15）同名的新用户组|
> |-r|	创建系统账户|	将此用户标记为系统账户。系统账户通常不能用于普通交互式登录，且其 UID（用户ID）通常小于 1000（或 500），以与普通用户区分开，适用于运行服务|
> |-s /bin/bash|	指定登录 Shell|	将用户的登录 Shell 设置为 /bin/bash。尽管是系统用户，但在 > 需要以该用户身份进行脚本执行或调试时，有一个可用的 Shell 是必要的|
> |odoo15|	新用户名|	指定要创建的用户名|
> 

## Step 3: 安装和配置Postgres数据库
> **使用docker-compos.yml** 
> ```yml
> version: '3.5'
> services:
> 	
> 	db:
> 		image: postgres:10
> 		ports:
> 			- "5432:5432"
> 		environment:
> 			- POSTGRES_DB=postgres
> 			- POSTGRES_USER=odoo
> 			- POSTGRES_PASSWORD=odoo
> 			- PGDATA=/var/lib/postgresql/data/pgdata
> 		volumes:
> 			- odoo-db-data:/var/lib/postgresql/data/pgdata
> volumes:
> 	odoo-db-data:
> ```
> 
> **本地安装Postgres**
> ```bash
> sudo apt install postgresql
> ```
> 
> ```bash
> sudo su - postgres -c "createuser -s odoo15"
> ```
> |部分|含义|解释|
> |---|---|---|
> |sudo|	提升权限|	以超级用户（root）身份执行后续命令|
> |su - postgres|	切换用户|	切换到 postgres 用户（这是 PostgreSQL 数据库在 Linux 系统上的默认管理员用户）。重点： 这一步是为了让命令以数据库管理员的身份执行|
> |-c "..."|	执行命令|	在切换用户后，立即执行引号内的命令，执行完毕后切换回原用户。|
> |"createuser -s odoo15"|	数据库命令|	这是在 PostgreSQL 内部执行的命令：|
> ||createuser|	用于在 PostgreSQL 中创建新的数据库角色/用户|
> ||-s|	赋予新创建的用户 odoo15 超级用户 (superuser) 权限。在 Odoo 的首次设置和运行时，通常需要此权限来创建和管理 Odoo 数据库|
> ||odoo15|	指定要在 PostgreSQL 中创建的数据库用户名（角色名）|
> 
>  

## Postgres数据库操作, pgadmin4 工具

> **用户保存数据位置**
> 1. Databases > [ production_db ] > Schemas > Public > Tables > res_users
> 2. 右键点击 res.users > view/edit data > first 100 
> 

## Odoo 配置日志
在 odoo.conf 配置文件中
> ```conf
> # 指定保存日志位置
> logfile = /var/log/odoo/odoo.log
> 
> # 日志级别 critical, error, warn, debug
> log_level = info 
> ```

> [!IMPORTANT]
> - 需要在 docker-compose.yml 中的 volumes 需要添加 `- ./odoo-log-data:/var/log/odoo`
> - `./odoo-log-data` 配置权限 `sudo chmod -R 777 odoo-log-data`
> 

保持追踪记录
> ```bash
> tail -f odoo-log-data/odoo.log
> ```
> 
> 