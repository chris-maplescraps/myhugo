+++
title = 'Ubuntu 22.04'
date = 2025-10-16T21:39:45+08:00
draft = true
slug = "45e4824"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Linux Ubuntu

### 基础操作命令
> 


### 安装 docker & docker compose
> 1. 移除旧的docker版本
>> ```bash
>> sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-compose-v2 docker-doc podman-docker containerd runc | cut -f1)
>> ```
>

> 2. Set up Docker's `apt` repository.
> > ```bash
> > # Add Docker's official GPG key:
> > sudo apt update
> > sudo apt install ca-certificates curl
> > sudo install -m 0755 -d /etc/apt/keyrings
> > sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o 
> > /etc/apt/keyrings/docker.asc
> > sudo chmod a+r /etc/apt/keyrings/docker.asc
> > 
> > # Add the repository to Apt sources:
> > sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
> > Types: deb
> > URIs: https://download.docker.com/linux/ubuntu
> > Suites: $(. /etc/os-release && echo 
> > "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
> > Components: stable
> > Signed-By: /etc/apt/keyrings/docker.asc
> > EOF
> > 
> > sudo apt update
> > ```
>

> 3. Install the Docker packages.
>> ```bash
>> sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
>> ```
> 

> [!NOTE]
> The Docker service starts automatically after installation. To verify that Docker is running, use:
> ```bash
> sudo systemctl status docker
> ```
> Some systems may have this behavior disabled and will require a manual start:
> ```bash
> sudo systemctl start docker
> ```
> ---

> 4. Verify that the installation is successful by running the `hello-world` image:
>> ```bash
>> sudo docker run hello-world
>> ```
>

> [!TIP]
> - docker-compose 属于旧版本，新版本docker compose 之间没有杠 -
> 