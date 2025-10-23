+++
title = 'Chatbox AI'
date = 2025-10-23T09:25:06+08:00
draft = false
slug = "071075e"
description = ""
summary = ""
tags = [ "技术", "AI" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Chatbox AI

##### 使用Deepseek 部署个人AI聊天机器人

> [!NOTE]
> 下载 https://ollama.com/    
> 下载 https://chatboxai.app/en  

#### 步骤一  安装Ollama

在Ollama官方网页，点击 **Models**，在搜索框输入 **deepseek** ，选择自己需要的版本

{{< figure src="/images/ollama_1.png" alt="xxx" caption="xxx" link="" class="w-50 ma0" >}}

点击想要的版本

{{< figure src="/images/ollama_2.png" alt="xxx" caption="xxx" link="" class="w-75 ma0" >}}

在右上角拷贝模型命令

{{< figure src="/images/ollama_3.png" alt="xxx" caption="xxx" link="" class="w-75 ma0" >}}

打开终端cmd，右键点击，会自动粘贴到终端，然后 `enter`

{{< figure src="/images/ollama_4.png" alt="xxx" caption="xxx" link="" class="w-75 ma0" >}}

等待下载安装。。。

{{< figure src="/images/ollama_5.png" alt="xxx" caption="xxx" link="" class="w-50 ma0" >}}

查看已经安装的模型 --> `ollama list` 

{{< figure src="/images/ollama_6.png" alt="xxx" caption="xxx" link="" class="w-50 ma0" >}}

运行模型 --> ollama run < 模型名称 >  
例如，运行deepseek-r1:7b  -- ollama run deepseek-r1:7b   

{{< figure src="/images/ollama_7.png" alt="xxx" caption="xxx" link="" class="w-50 ma0" >}}

停止运行模型 --> `ctrl + d`

{{< figure src="/images/ollama_8.png" alt="xxx" caption="xxx" link="" class="w-50 ma0" >}}



> [!TIP]
>
> 查看Ollama命令  
> 在终端 cmd / powershell 输入`ollama -h`

#### 步骤二  安装 Chatbox AI



