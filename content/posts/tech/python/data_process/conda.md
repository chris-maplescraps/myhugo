+++
title = 'Conda'
date = 2025-11-07T10:12:25+08:00
draft = false
slug = "98b6139"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Conda  
### 下载 + 安装 Ananconda
> - 点击 **anaconda 官方链接**：[official anaconda](https://www.anaconda.com/download/success)  
> - 选择下载 **Distribution Installers**  
> - 下载完毕，点击 **anaconda installer** 开始安装， 等待安装完成  
> 

---

### 添加 Conda 环境变量
> 1. 若在安装时**勾选添加环境变量**，会在用户环境变量的Path中添加相应路径；  
> 若安装时没有勾选添加环境变量，则需要在安装后手动添加环境变量。  
> Windows操作系统下同时按下“Win+S”打开搜索栏，搜索“编辑系统环境变量”可进入查看和编辑环  境变量。  
> {{< figure src="/images/image-20250620164419520.png" alt=“xxx” >}}  
> 
> 2. 单击右下角环境变量，双击上半部分 **用户变量中的Path** ，若先前安装时勾选了添加环境变量，在此可查看到已添加的路径。  
> {{< figure src="/images/image-20250620164544069.png" alt=“xxx” >}}
> 
> 3. 若先前安装时未勾选添加环境变量，则需找到先前安装时设定的Anaconda安装路径。此处为`D:\ProgramFiles\anaconda3`，需对照自己的安装路径，在环境变量中点击“新建”依次添加如下路径：  
> ```
> D:\ProgramFiles\anaconda3
> D:\ProgramFiles\anaconda3\Library\mingw-w64\bin
> D:\ProgramFiles\anaconda3\Library\usr\bin
> D:\ProgramFiles\anaconda3\Library\bin
> D:\ProgramFiles\anaconda3\Scripts
> ```
> 
> 4. 按下 `Win+R`，输入 `cmd`，点击确定，打开命令提示符
> {{< figure src="/images/image-20250620165046595.png" alt=“xxx”  class=“” >}}
> 
> 5. 输入conda info查看conda信息，输入`python --version`查看Python版本。Anaconda安装成功。  
> {{< figure src="/images/终端测试.png" alt=“xxx”   >}}
> 

---

### Conda 常用命令
```shell
conda -help            # 查看帮助
conda info             # 查看 conda 信息
conda --version        # 查看 conda 版本
conda update conda     # 更新 Conda (慎用)
conda clean -all      # 清理不再需要的包
conda <指令> --help     # 查看某一个指令的详细帮助
conda config --show    # 查看 conda 的环境配置
conda clean -p         # 清理没有用, 没有安装的包
conda clean -t         # 清理 tarball
conda clean --all      # 清理所有包和 conda 的缓存文件
```

---

### Conda 环境管理
> ##### 创建 Conda 虚拟环境
>> 使用 conda可以在电脑上创建很多套相互隔离的 Python环境，命令如下：  
>> ```shell
>> # 语法
>> conda create --name <env_name> python=<version> [package_name1] [package_name2] [……]
>> 
>> # 样例 创建一个名为 myenv 的环境, python 版本为3.10
>> conda create --name myenv python=3.10 # --name 可以简写为 -n
>> ```

> ##### 切换 Conda环境
> > 前面说到 Conda可以创建多套相互隔离的 Python环境，使用 `conda activate env_name` 可以切换不同的环境。  
> > ```shell
> > # 语法
> > conda activate env_name
> > 
> > # 样例 切换到 learn 环境
> > conda activate learn
> > ```
>

> > 
> > 如果要退出此环境，回到基础环境，可以使用如下命令
>
> > ```shell
> >  #退出当前环境
> > conda deactivate
> > ```
>

> ##### 查看已创建的 Conda 虚拟环境
>> 当电脑上安装了很多台 Conda环境的时候，可以使用 `conda env list` 命令查看所有已创建的 Conda环境。  
>> ```shell
>> # 查看当前电脑上所有的 conda环境
>> conda env list
>> ```
>> 

> ##### 删除某个 Conda 虚拟环境  
> > ```shell
> > # 语法
> > conda remove --name <env_name> --all
> > 
> > # 样例
> > conda remove --name learn --all
> > ```
>

> ##### 克隆 Conda 虚拟环境
> > ```shell
> > # 语法
> > conda create --name <new_evn_name> --clone <old_env_name>#样例
> > conda create --name myclone --clone myenv
> > ```
>

### Conda 管理包
一旦激活了环境，你就可以使用 `conda`和 `pip`在当前环境下安装你所需要的包。在conda环境中, 不建议使用 `pip`。  
> ##### 安装包
>> 在激活的环境中安装包，例如安装NumPy：
>> ```bash
>> conda install numpy
>> ```
>> 可以使用以下命令安装特定版本的包：
>> ```bash
>> conda install numpy=1.18
>> ```
>> 

> ##### 更新包
> > 更新某个包到最新版本：
> > ```shell
> > conda update numpy
> > 
> > # 更新所有包到最新版本 (慎用)
> > conda update --all  
> > 
> > 执行命令后，conda将会对版本进行比较并列出可以升级的版本。同时，也会告知用户其他相关包也会升级到相应版本。当较新的版本可以用于升级时，终端会显示Proceed([y]/n)? , 此时输入y 即可进行升级。
> > ```

> ##### 卸载包
>> 如果不再需要某个包，可以将其卸载：
>> ```shell
>> conda remove numpy
>> ```
>> 
>> ##### 列出环境中的所有包
>> ```shell
>> conda list
>> ```
>> 
>> 查看当前虚拟环境中已安装的某个包的信息
>> ```shell
>> conda list pip
>> ```
>> 

> ##### 搜索包
>> 搜索可用的包及其版本信息：
>> ```shell
>> conda search package-name
>> ```
>> 

### Pycharm 使用 Conda
> 1. 使用 conda 创建项目所需要的虚拟环境
> ```
> conda create -n llamaindex-rag python=3.xx
> ```
> 2. 创建项目，选择自定义环境，类型选择Conda，环境选择 llamaindex-rag，点击 **创建** 即可
> 

---

- 关于更多jupyter：点击 [阅读 jupyter 文章]({{< relref "jupyter.md" >}}) 