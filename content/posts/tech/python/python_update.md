+++
title = 'Python Update'
date = 2025-10-16T10:32:06+08:00
draft = false
slug = "460fa21"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Latest version

## Python 3. 14
- no GIL | 官方名字 free threaded
- 2 个版本 --> with GIL | without GIL ( default with GIL )

> [!NOTE]
>
> #### GIL： Global Interpreter Lock 全局解释器  
> #### 核心作用： 在任何给定的时间点，它只允许 **一个** 线程执行 Python **字节码**  
>
> > 想象一下，GIL 就像是厨房里唯一的**厨师帽**。无论厨房里有多少个厨师（线程）在工作，只有戴着帽子的那位才能在灶台（CPU）前切菜、炒菜（执行 Python 代码）。其他厨师必须等着，直到戴帽子的人把帽子摘下。
>
> #### 为什么需要：   
>
> 1. 简化 CPython 的实现 (Simplicity)：   
>    Python 的内存管理（尤其是**引用计数**）和垃圾回收机制得到了简化。如果没有 GIL，开发者必须在 CPython 的底层代码中处处使用复杂的细粒度锁来确保内存安全，这会让解释器的开发难度大大增加。   
> 2. 更容易集成 C 库 (C Extensions)：  
>    许多常用的 Python 扩展库（如 NumPy、SciPy）都依赖于 C 语言库。在有 GIL 的情况下，这些 C 扩展可以更容易地编写，因为它们不必担心 Python 解释器内部的并发问题。

> [!TIP]  新特征
>
> 1. 模板字符串字面值 (Template String Literals)   
>    模板字符串字面值是一种新的字符串类型，旨在简化**字符串插值 (interpolation)** 和**国际化 (i18n)** 场景。它引入了一个新的字符串前缀 `t` or `T` (t-string)，类似 `f` (f-string) 或 `r` (raw string)
>
>    ```python
>    name = "Alice"
>    greeting = t"Hello, ${name}!" 
>    print(greeting)
>    # 输出预计为: Hello, Alice!
>    ```
>
>    > 新特性主要有两个核心目标：   
>    >
>    > 1. **更清晰的插值语法 (`${...}`):**
>    >
>    >    - 它使用 **`${identifier}`** 语法进行变量替换，这与许多其他编程语言（如 JavaScript 的模板字面量或 Shell 脚本）的插值语法更为一致。  
>    >       
>    >
>    >    - 这解决了 f-string 在某些情况下可能过于强大（它能运行任意 Python 表达式）和引起安全顾虑的问题。模板字符串默认只替换**标识符 (identifiers)**，更安全、更受限。