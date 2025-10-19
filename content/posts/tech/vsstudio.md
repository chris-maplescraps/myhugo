+++
title = 'VS Studio'
date = 2025-10-19T10:42:43+08:00
draft = false
slug = "aeede5e"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

### Vs Studio installation
> Install VS Studio Code
> ```bash
> sudo apt update
> 
> Option 1
> sudo apt-get install wget gpg
> wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
> sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
> echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
> rm -f packages.microsoft.gpg
>
> sudo apt update
>
> sudo apt install code
>