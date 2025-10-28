+++
title = 'Numpy'
date = 2025-10-28T14:34:29+08:00
draft = false
slug = "2360db1"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Numpy  
<br>  

#### 什么是numpy?  
> - **numpy** 是 **Python** 科学计算基础包  用于对数组进行快速操作的各种方法，包括数学，逻辑，形状操作，排序，选择，I/O，离散傅里叶变换，基本线性代数，基本统计运算，随机模拟等等  
> - ndarray，有矢量算术运算 + 复杂广播能力 + 快速 + 节省空间的多维数组
> - 标准数学函数
> - 对磁盘数据 + 内存映射文件的工具
> - 线性代数，随机数生成 + 傅里叶变换
> - 由 C，C++，Fortran等语言编写的API
> 

#### ndarray 核心特性  
> - **多维性**：支持 0 维（标量），1 维度（向量），2 维（矩阵） + 更高数组  
> - **同质性**：所有元素类型必须一致（由 **dtype** 指定）  
> - **高效性**：连续内存块存储，支持向量化运算  
> 

#### ndarray 属性
|属性名称|通俗解释|使用示例|
|---|---|---|
|shape|数字形状：行数和列数（或更高维度的尺寸） |arr.shape |
|ndim|维度数量：数组是几维（1维，2维，3维）|arr.ndim|
|size|总元素个数：数组中所有元素的总数|arr.size|
|dtype|元素类型：数组中元素的类型（整数，浮点数等）|arr.dtype|
#### 不常用的进阶属性
|T|转置：行变列，列变行|arr.T|
|itemsize|单个元素占用的内存字节数|arr.itemsize|
|nbytes|数组总内存占用量：size * itemsize|arr.nbytes|
|flags|内存存储方式：是否连续存储（高级优化）|arr.flags|

#### ndarray 创建
|用途||方法|
|---|:---:|:---:|:---:|:---:|
|**基础构造**| np.array()|np.copy()|||
|**预定义形状填充**|np.zeros()|np.ones()|np.empty()|np.full()|
|**基于数值范围生成**|np.arrange()|np.linspace()|np.logspace()|
|**特殊矩阵生成**|np.eye()|np.diag()|
|**随机数组生成**|np.random.rand()|np.random.randn()|np.random.randint()|
|**高级构造方法**|np.array()|np.loadtxt()|np.fronfunction()|

> 
> 
> 
> 
> 
> 
> 