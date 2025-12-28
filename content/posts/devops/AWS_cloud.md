+++
title = 'AWS_cloud'
date = 2025-12-28T20:27:57+08:00
draft = false
slug = "b9ef132"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# AWS_cloud

## AWS account
> :one: 创建 aws root 账号，用于创建 IAM 账号
> {{< figure src="/images/create_root_account.png"  class="w-75 ma0" >}}
> :two: 选择 Sign in using root user email
> {{< figure src="/images/IAM login.png"  class="w-75 ma0" >}}
> :three: 输入 root 账号邮箱登录
> {{< figure src="/images/root_login.png"  class="w-75 ma0" >}}
> :four: 点击左上角菜单栏  >  Security, Identity & Compliance > IAM 创建别名
> {{< figure src="/images/create_alias.png"  class="w-75 ma0" >}}
> :five: 开通编程和控制台权限, 登录 root 用户 > Users > username_name > Security Credential > Access key > select other
> {{< figure src="/images/open_permission_1.png"  class="w-75 ma0" >}}
> {{< figure src="/images/open_permission_2.png"  class="w-75 ma0" >}}
> {{< figure src="/images/open_permission_3.png"  class="w-75 ma0" >}}
> {{< figure src="/images/open_permission_4.png"  class="w-75 ma0" >}}
> {{< figure src="/images/open_permission_5.png"  class="w-75 ma0" >}}
> 

## Create EC2 Instance
> 


## Systems Manager (SSM) login
##### 第一步：为 EC2 实例配置 IAM 角色
> :one: EC2 默认没有权限与 SSM 服务通信，你需要给它一个“身份证”
> :two: 打开 **IAM 控制台**
> :three: 点击 **角色 (Roles)** -> **创建角色 (Create role)**
> :four: 选择 **AWS 服务**，并在**服务下拉列表中选择 EC2**
> :five: 在**权限策略**搜索框中输入：**AmazonSSMManagedInstanceCore**，勾选该策略
> :six: 给角色起个名字（例如：EC2-SSM-Role），点击创建
> :seven: 回到 **EC2 控制台**，**勾选你的实例 -> 操作 (Actions) -> 安全 (Security) -> 修改 IAM 角色**，选择你刚刚创建的 **EC2-SSM-Role**
> 

##### 第二步：检查安全组 (Security Group)
> 使用 SSM 登录的一个巨大优势是：你可以关闭安全组中的所有入站规则
> - SSM Agent 是从实例内部“主动”连接到 AWS 服务端的（Outbound）
> - 只要你的实例能访问互联网（通过 NAT 网关或公网 IP），你就不需要在安全组里开启 22 端口。这极大地降低了被暴力破解的风险
> 

##### 第三步：如何执行登录
> 方法 A：直接通过 AWS 控制台（最快）
> :one: 在 EC2 实例列表勾选你的实例
> :two: 点击右上角的 连接 (Connect)
> :three: 选择 Session Manager 选项卡，点击 连接
> :four: 你将直接在浏览器中获得一个终端
> 

> 方法 B：通过本地命令行（体验最好）
> :one: 安装 AWS CLI 并配置好你的 Access Key
> :two: 安装插件：下载并安装 Session Manager Plugin
> :three: 运行命令：
> ```bash
> # 使用实例 ID 登录（推荐）
> aws ssm start-session --target i-0123456789abcdef0
> ```

>> 注意事项
>> - 网络通畅：如果你的实例在私有子网（Private Subnet）且没有 NAT 网关，SSM 会失效。这种情况下需要配置 VPC Endpoints
>> - 操作系统：Amazon Linux 2/2023 默认自带 Agent。如果是 Ubuntu 或 Windows，可能需要手动安装 amazon-ssm-agent