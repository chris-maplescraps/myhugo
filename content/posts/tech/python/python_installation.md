+++
title = 'Python Installation'
date = 2025-10-16T13:26:19+08:00
draft = false
slug = "e5febaf"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Python Installation

## 💻 Linux Ubuntu

#### Step 1

> ```bash
> sudo add-apt-repository ppa:deadsnakes/ppa
> sudo apt update
> sudo apt install python3.x
> sudo python3 --version
> ```
>
#### Step 2
> Install VS Studio Code
> ```bash
> sudo apt update
> 
> Option 1
<<<<<<< HEAD
> sudo apt install software-properties-common apt-transport-https wget
> wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
> sudo add-apt-repository "deb [arch=amd64] > https://packages.microsoft.com/repos/vscode stable main"
> sudo apt update
> sudo apt install code
> 
> 
> Option 2
=======
>>>>>>> 7d315be (create vs_studio.md)
> sudo apt-get install wget gpg
> wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
> sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
> echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
> rm -f packages.microsoft.gpg
<<<<<<< HEAD
> ```
=======
>
> sudo apt update
>
> sudo apt install code
>>>>>>> 7d315be (create vs_studio.md)
>

## 💻 WindowsOS

#### Step 1
> a. Download python installer https://www.python.org/downloads/
> 

#### Step 2
> Download & Install Pycharm https://www.jetbrains.com/pycharm/download/?section=windows