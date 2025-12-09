+++
title = 'Python Knowledge'
date = 2025-10-16T15:56:15+08:00
draft = false
slug = "48d997b"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Python Knowledge
> [!NOTE]+
> - 编译器 compiler =  将源代码文件转换成可行执行二进制文件
> - 解释器 interpreter =  将源代码直接执行，无需进行转换
> - 源代码 source code = 无法直接被电脑运行，需要被编译 或者 解释
> - 高级语言 high-level programming =  由人类进行编写，然后选择使用编译器还是解释器
> - 自然语言 natural language = 人类沟通语言  
> - 机器语言 machine language = 1byte = 8 bits ( 二进制 0 和 1 )

> ### Python 原理机制  
> #### 类继承结构（Class Inheritance Hierarchy）  
> #### 🧩 什么是「类继承结构」？  
> 🟦 1️⃣ **基本概念 **  
> 在 Python 中，**类（class）**  可以从另一个类 **继承（inherit）** 功能。  
> 👉 继承的意思是：  
>> “子类可以直接使用父类的属性和方法，而不需要重新写一遍。”   
> #### 🧠 举个简单例子： 
> > ```python
> > class Animal:  # 父类（基类）
> >    def eat(self):
> >        print("动物会吃东西")
> >
> > class Dog(Animal):  # 子类（继承 Animal）
> >    def bark(self):
> >        print("狗在汪汪叫")
> >
> > dog = Dog()
> > dog.eat()   # 继承自 Animal
> > dog.bark()  # 自己的方法
> > ```
>> 输出：
>> ```txt
>> 动物会吃东西
>> 狗在汪汪叫
>> ```
>>
>> 🟩 说明：   
>> - `Dog` 继承了 `Animal` 的行为（ `eat()` 方法 ）
>> - 如果 `Dog` 自己没有 `eat()`，就去它的父类 `Animal` 里找
>> - 这就是所谓的 **类继承结构**
>
>> 🟨 2️⃣ **多层继承（层级关系）**   
>> Python 允许多层继承，比如：   
>> ```python
>> class A: pass
>> class B(A): pass
>> class C(B): pass
>
>> 📜 类继承结构（Class Hierarchy）如下：   
>> ```css
>> C → B → A → object
>> ```
>> 你可以通过 __base__ 或 __mro__ 查看继承关系：
>> ```python
>> print(C.__mro__)
>> ```
>> 输出：
>> ```kotlin
>> (<class '__main__.C'>, <class '__main__.B'>, <class '__main__.A'>, <class 'object'>)
>> ```
>
>> 🟧 3️⃣ 所有类的最终祖先：object   
>> 无论你写的类多复杂，   
>> Python 中所有类的最顶层父类都是 object
>> ```python
>> class A: pass
>> print(issubclass(A, object))  # True
>> ```
>> 📘 这意味着：
>>> Python 里“一切皆对象（Everything is an object）”
>
> #### 🟥 二、什么是「内置异常（Built-in Exceptions）」   
>> 这些异常其实就是一套预定义的类   
>> #### 🧠 举个例子：
>> ```python
>> print(1 / 0)
>> ```
>> 输出：
>> ```vbnet
>> ZeroDivisionError: division by zero
>> ```
>> 📘 `ZeroDivisionError` 是一个类，它继承自 `ArithmeticError`，   
>> 而 `ArithmeticError` 又继承自 `Exception`，   
>> `Exception` 再继承自 `BaseException`。   
>> 这就是异常的 **继承结构**（就像家谱一样）。   
>
> #### 🧱 三、Python 内置异常的继承结构（简化版）
>> ```php
>> BaseException                     ← 所有异常的根类
>> ├── SystemExit                    ← 程序退出（系统用）
>> ├── KeyboardInterrupt             ← 用户按 Ctrl + C
>> ├── Exception                     ← 所有常规错误的父类
>> │   ├── ArithmeticError            ← 算术错误类
>> │   │   ├── ZeroDivisionError      ← 除以零
>> │   │   ├── OverflowError          ← 数字太大
>> │   │   └── FloatingPointError     ← 浮点错误
>> │   ├── OSError                   ← 操作系统错误
>> │   │   ├── FileNotFoundError      ← 文件不存在
>> │   │   ├── PermissionError        ← 权限不足
>> │   │   ├── IsADirectoryError      ← 路径是目录
>> │   │   └── NotADirectoryError     ← 非目录路径
>> │   ├── ValueError                ← 值错误
>> │   ├── TypeError                 ← 类型错误
>> │   ├── KeyError                  ← 字典键错误
>> │   ├── IndexError                ← 索引超出范围
>> │   ├── LookupError               ← 查找类错误（父类）
>> │   │   └── UnicodeDecodeError     ← 解码错误
>> │   └── RuntimeError              ← 运行时错误（通用）
>> └── GeneratorExit                 ← 生成器关闭
>> ```
>> 📘 注意：   
>> - 所有常见错误都在 **Exception** 分支下   
>> - 系统级错误（例如 `KeyboardInterrupt` ）在 **BaseException** 分支下   
> #### 🟩 四、如何查看一个异常的继承结构（实践）
>> ```python
>> def show_exception_hierarchy(err):
>>     cls = err
>>     while cls:
>>         print("↳", cls.__name__)
>>         cls = cls.__base__
>> 
>> show_exception_hierarchy(FileNotFoundError)
>> ```
>> 输出：   
>> ```php
>> ↳ FileNotFoundError
>> ↳ OSError
>> ↳ Exception
>> ↳ BaseException
>> ↳ object
>> ```
>> 📜 这条链清楚展示了继承关系。
> #### 🧠 五、类继承结构 和 内置异常 的关系
>> ✅ 本质上：
>>> “异常类 只是 Python 普通类体系的一部分。”
>> 也就是说：   
>> - 异常类之间的关系 → 就是类继承结构
>> - 捕获异常时的行为 → 就依赖继承结构进行“向上匹配”
> 🧩 举例说明：
>> ```python
>> try:
>>     open("不存在.txt")
>> except OSError:
>>     print("OSError 捕获成功")
>> except FileNotFoundError:
>>     print("FileNotFoundError 捕获成功")
>> ```
>> 输出：
>> ```nginx
>> OSError 捕获成功
>> ```
>> 📘 原因：   
>> - FileNotFoundError 是 OSError 的子类   
>> - Python 捕获异常时，会从上往下匹配继承链   
>> 
>> 🟨 所以顺序必须是：
>> ```python
>> except FileNotFoundError:
>> except OSError:
>> ```
>> 👉 先捕获子类，再捕获父类！
>
>> #### 🎨 总结（记忆彩色卡）
>> | 概念       | 含义                     | 举例                                        |
| -------- | ---------------------- | ----------------------------------------- |
| 🟦 类继承结构 | 类之间的“血缘关系”，谁继承谁        | `Dog → Animal → object`                   |
| 🟩 内置异常  | Python 自带的错误类体系        | `FileNotFoundError → OSError → Exception` |
| 🟨 最顶层类  | 所有异常的根：`BaseException` | 捕获所有错误                                    |
| 🟥 最常用父类 | `Exception`（开发者一般捕获这个） | `except Exception as e:`                  |
| 🟧 系统异常  | 比如 `KeyboardInterrupt` | 不要轻易捕获                                    |
> 
> 💬 一句话总结
>> ✅ “类继承结构是类与类之间的层次关系，   
>> Python 的所有异常都是一棵继承树上的节点，   
>> 它们最终都源自 **BaseException**。”    
>

> ### Python 语法
>
> ```python
> print("hello python!!!")
> ```
> 
---
> ### 变量
>
>> a = "John"  
>> b = 123  
>> c = 3.142  
>> d = True  
>> e = [ "Superman", "Iron-man", "Ant-man" ]  
>> f = { "Price": 50.00, "Item": "iPhone" }  
---
> ### 注释
> 
---
> ### 条件判断 
> 
---
> ### 数据类型
> > ##### List 列表
> > - 使用切片 slide 分割列表，将创建新的内存地址和原本的地址不相同
>
>
> > ##### 列表生成式 List comprehension
> > ```python
> > squares = [ expression for element in list if conditional ]
> > squares = [ x ** 2 for x in range(10) ]
> > 
> > for element in list:
> >  if conditional:
> >      expression
> >         
> > for x in range(10):        
> >  if x == 0:    
> >      break
> > ```
>
---
> > ##### 索引嵌套
> > ```python
> > numbers = [2, 3, 5, 8]
> > numbers[numbers[1]] # 属于嵌套索引表达式
> > # 拆解内部索引，再拆解外部索引
> > # 内部的索引 1 是 3 --> numbers[1] = 3
> > # 外部的索引 3 是 8 --> numbers[3] = 8
> > 
> > numbers[-numbers[3]]
> > # 内部的索引 3 是 8 --> -numbers[3] = -8
> > # 外部的索引 -8 是 unknown --> numbers[-8] = Error
> > 
> > numbers[3:3]
> > # 切片索引 开始3 结束3，返回结果空列表
> > 
> > numbers[numbers[3]]
> > # 拆解内部索引，再拆解外部索引
> > # 内部的索引 3 是 8 --> numbers[3] = 8
> > # 外部的索引 8 是 unknown --> numbers[8] =Error
> > ```
>
> > ---
>
> > ##### 二维列表生成式
> > ```python
> > # Pattern 1
> > matrix = [[0 for c in range(3)] for r in range(4)]
> > 
> > # Pattern 2
> > matrix = [[(r, c) for c in range(3)] for r in range(4)]
> > ```
>
> > 输出：
> > ```output
> > # Pattern 1
> > [[0, 0, 0]], [[0, 0, 0]], [[0, 0, 0]], [[0, 0, 0]]
> > 
> > # Pattern 2
> > [[(0, 0), (0, 1), (0, 2)]], [[(1, 0), (1, 1), (1, 2)]], [[(2, 0), (2, 1), (2, 2)]], [[(3, 0), (3, 1), (3, 2)]]
> > ```
> > ---
>

> ### 循环 & 嵌套循环
> ##### while 语法结构说明：
> ```python
> # 初始条件设置 = 一般是重复执行的 计数器，不然会无限循环
> 
> while 条件（ 判断 计数器 是否条件成立 ）：
> 	条件成立后执行的代码 1
> 	条件成立后执行的代码 2
> 	条件成立后执行的代码 3
> 	条件成立后执行的代码 4
> 
> 	处理条件（计数器 + 1）
> ```
> ---
> ##### for 语法结构说明：
> ```python
> for 变量 in sequences:
> 	print( 变量 )
> for 变量 in range(x):
> 	print( 变量 )
> for 变量 in range(x, y, z):
> 	print( 变量 )
> ```
>
> ##### while & else 组合
> **1. for 循环中的 else 块**
>
> > else 块会在 循环正常执行完毕（即遍历完所有元素）时执行。
> > 如果循环被 break 语句中断，则 else 块不会执行。
>
> **2. while 循环中的 else 块**
> > else 块会在 循环条件变为假 时执行。
> > 如果循环被 break 语句中断，则 else 块不会执行。
>
---
> ### 函数
> ##### return 语句的基本语法
> ```python
> def 函数名(参数列表):
> 	代码块
> 	return 返回值
> ```
> > [!NOTE]
> > 说明：
> > - 如果没有 return 语句，默认返回 None， None 是内置常量，代表空值对象
> > - 既然是一个值。就代表有自己的内存空间 ID
---
> ### 数据驻留机制
> ##### 驻留机制成立条件
> :one: 字符串是由 26 个英文字母大小写，0-9，_组成
> :two: 字符串长度为 0 或者 1 的时候
> :three: 字符串在编写代码的时候才会进行驻留，不是在运行代码的时候
> :four: [ -5, 256 ] 的整数数字
> ##### sys.intern() 可以实现强制驻留
> ```python
> import sys
> a = "!@#
> b = "!@#
> print(id(a)) # 233291254
> print(id(b)) # 233291523
> 
> # 将变量 b 指向 变量 a 相同内存
> b = sys.intern(a)
> print(id(b)) # 233291254 变量 a 内存地址
> ```
> > [!NOTE]
> > - 如果 a 和 b 的值不同，当强制将 b 指向 a，那么 b 的值也会和 a 一样
> > - 参考视频 [bilibili 韩顺平 - 驻留机制](https://www.bilibili.com/video/BV1zN4y1v7Vv?spm_id_from=333.788.videopod.episodes&vd_source=5f93ceb15a68557ff6f7a1f95aca67bb&p=29)
---
> ### 函数调用机制
> 
> 参考视频
---
> ### 函数传参机制
> 
> 
---
> ### 函数递归机制
> - 函数调用自己，每次调用的时候传入不同的值
> - 有助于解决复杂问题，也能让代码更简洁
> - 必须有 base case 决定终止条件，否则会无限调用函数，直到栈溢出（当调用函数，会在内存创建新的栈）
> ---
> ##### 递归执行过程分为 "递进" 和 "回归"
>
> {{< figure src="/images/recursive.png" alt="xxx" class="w-75 ma0" >}}
> 
> 
> > [!NOTE]
> > - 参考视频 [林粒粒呀 - 8分钟搞懂“编程的鬼打墙”——递归](https://www.bilibili.com/video/BV14q5fzAEpD/?spm_id_from=333.337.search-card.all.click&vd_source=5f93ceb15a68557ff6f7a1f95aca67bb)
>
---
> ### 实参 & 形参
> 
---
> ### 异常模块
> 
---
> ### 内置函数
> 
---
> ### 泡泡排序
> ```python
> # 创建一个名为 my_list 的列表（List），并存入初始数据 [8, 10, 6, 2, 4]。这就是我们要排序的目标
> my_list = [8, 10, 6, 2, 4]
> 
> # 创建一个布尔, 为 True 才能启动下面的 while 循环
> swapped = True
> 
> # 开始执行 while 循环
> while swapped:
> 
> 		# 假设这一轮遍历不会发生交换，就会退出 while 循环，不然会死循环
> 		swapped = False  # no swaps so far
> 		
> 		# 遍历列表的索引，能够比较 (索引0, 索引1)、(索引1, 索引2)、(索引2, 索引3) 和 (索引3, 索引4)
> 		for i in range(len(my_list) - 1):
> 		
> 			# 比较列表中的右边邻居元素
> 			# 检查当前元素 (my_list[i]) 是否大于 下一个元素 (my_list[i + 1])
> 			# 在第一轮 i=0 时，它会检查 my_list[0] (即 8) 是否大于 my_list[1] (即 10)
> 			if my_list[i] > my_list[i + 1]:
> 			
>				# 只有在 if 条件为 True 时才执行, 将 swapped 变量设置回 True
> 				swapped = True  # a swap occurred!
> 				
> 				# my_list[1] 和 my_list[1 + 1] 原始列表位置 [10, 6]
> 				# 当 i=1 时 (10 > 6)，列表从 [x, 10, 6, x, x] 变为 [6, 10]
> 				my_list[i], my_list[i + 1] = my_list[i + 1], my_list[i]
> 
> print(my_list)
> ```
---
> ### 类
> 
---
> ### 面向对象
> 
---
> ### 装饰器
> > 🧩 一、装饰器（Decorator）是什么？  
> > 👉 **装饰器本质上是一个“函数”，它的作用是给另一个函数或类添加功能，而不改动原本的代码。**  
> >> 可以理解为：  
> >> “在不改变原函数结构的前提下，给它加上一层外衣。”  
>
> > ✅ 普通函数装饰器示例
> > ```python
> > def log_decorator(func):
> >    def wrapper():
> >        print("📜 正在调用函数：", func.__name__)
> >        result = func()
> >        print("✅ 函数执行完成")
> >        return result
> >    return wrapper
> > @log_decorator     # 相当于 say_hello = log_decorator(say_hello)
> > def say_hello():
> > 	print("你好，Python！")
> > 	
> > say_hello()
> > ```
>
> > **输出结果：**
> >
> > ```
> > 📜 正在调用函数： say_hello
> > 你好，Python！
> > ✅ 函数执行完成
>
---
> ### 运算符家庭
> ##### 运算符优先级图表 ( 上（最高）-> 下（最低）)
> |运算符|描述|所属|
> |---|---|---|
> |( expressions... )| 加圆括号的表达式|算 Arithmetic|
> |**|乘方，次方|算 Exponentiation|
> |*，@，/，//，%|乘，矩阵乘，除，整除，取余|算 Multi / Division|
> | + -|加法减法|算 Add / Subtraction|
> |>> <<| 右移，左移运算符（移位）|位 Bitwise|
> |&|按位与|位 Bitwise|
> |^|按位异或|位 Bitwise|
> | \| | 按位或|位 Bitwise|
> |in，not in，is，is not，<，<=，>，>=，!=，==| 比较运算，包括成员检测和标识号检测|比 Comparison|
> |not x|布尔逻辑非 NOT|逻 Logical|
> |and|布尔逻辑与 AND|逻 Logical|
> |or|布尔逻辑或 OR|逻 Logical|
> |=，%=，/=，//=，-=，+=，*=，**=|赋值运算符|赋 Assignment|
>
> 
> > ##### 算数运算符
> > |运算符|运算|示例|结果|
> > |:---:|:---|:---:|:---:|
> > |**+**|加|5 + 5|10|
> > |**-**|减|6 - 4|2|
> > |**\***|乘|3 * 4|12|
> > |**/**|除|5 / 5|1|
> > |**%**|取模（取余）|7 % 5|2|
> > |**//**|取整除-返回商的整数部分（向下取整）|9 // 2|4|
> > ||向下取整 = 取最小的数值|-9 // 2|-5|
> > |**\*\***|返回 x 的 y 次幂|2 ** 4|16|
>
> >> ##### :green_book::green_book::green_book: 知识补充
> >> Python `7 % 5` 意味着 `7` 除以 `5` 的余数：
> >> $$
> >> 7 \bmod 5 = 2
> >> $$
> >> - 被除数 = 7
> >> - 除数 = 5
> >> - 商数 = 1
> >> - 余数 = 2
>
> >> Python `9 // 2` 意味着 `9` 除以 `2` 的向下取整的商数：
> >> $$
> >> \lfloor \frac{9}{2} \rfloor = \lfloor 4.5 \rfloor = 4
> >> $$
> >> - 被除数 = 9
> >> - 除数 = 2
> >> - 商数 = 4.5 向下取最小的数值 = 4
>
> >> ---
>
> >> Python `-9 // 2` 意味着 `-9` 除以 `2` 的向下取整的商数：
> >> $$
> >> \lfloor \frac{-9}{2} \rfloor = \lfloor -4.5 \rfloor = -5
> >> $$
> >> - 被除数 = 9
> >> - 除数 = 2
> >> - 商数 = -4.5 向下取最小的数值 = -5
>
> 
>
> > ##### 赋值运算符
> > |运算符|描述|实例|
> > |---|---|---|
> > |=|普通赋值运算符| c = a + b 将 a + b 的运算结果赋值给 c|
> > |+=|复合加法赋值运算符|c += a 等同于 c = c + a|
> > |-=|复合减法赋值运算符|c -= a 等同于 c = c - a|
> > |*=|复合乘法赋值运算符|c *= a 等同于 c = c * a|
> > |/=|复合除法赋值运算符|c /= a 等同于 c = c / a|
> > |%=|复合取模赋值运算符|c %= a 等同于 c = c % a|
> > |**=|复合幂赋值运算符|c **= a 等同于 c = c ** a|
> > |//=|复合取整除赋值运算符|c //= a 等同于 c = c // a|
>
> > ##### 比较运算符
> > - 结果是 __True__ 或者 __False__
> > - 常用在 __if__ 结构条件，__True__ 就执行代码块，__False__ 就不执行
> > ```python
> > n1 = 1
> > if n1 > -10:
> > 	print("hi...")
> > ```
> > |运算符|运算|示例|结果|
> > |---|:---:|---|---|
> > |==|等于|4 == 3|False|
> > |!=|不等于|4 != 3|True|
> > |<|小于|4 < 3|False|
> > |>|大于|4 > 3|True|
> > |<=|小于等于|4 <= 3|False|
> > |>=|大于等于|4 >= 3|True|
> > |is|判断两个变量引用对象是否为同一个内存地址|
> > |is not|判断两个变量引用对象是否不同内存地址|
>
>
> > ##### 逻辑运算符
> > |运算符|逻辑表达式|描述|实例|
> > |---|---|---|---|
> > |and| x and y | x 为 False，返回 x 的值，否则返回 y 计算值|( a and b ) 返回 20|
> > |or| x or y | x 为 True，返回 x 的值，否则返回 y 计算值| ( a and b ) 返回 10|
> > |not| not x | x 为 True，返回 False，x 为 False，返回 True| not ( a and b ) 返回 False
> > - 逻辑表达式是有 ( expression and expression )
>
>
> > ##### 三元运算符
> > ```python
> > a = 10
> > b = 80
> > c = 55
> > max = a if a > b else b
> > print(max)
> >
> > # 分段方式计算，可读性好
> > max1 = a if a > b else b
> > max2 = max1 if max1 > c else c
> > print(max2)
> >
> > # 嵌套方式计算，可读性差
> > max = (a if a > b else b) if (a if a > b else b) > c else c
> > print(max)
> > ```
> > 补充点
> > ```
> >      a if a > b else b
> >      |               |
> >    表达式           表达式
> > 如果条件成立 则返回表达式 a 值
> > 如果条件不成立 则返回表达式 b 值
> > ```
>
> > ##### 位运算符
> > ##### & 与运算 and
>
> > |运算符|逻辑表达式|描述|实例|
> > |---|---|---|---|
> > |\||or||||
> > |^|异或运算|||
> > |~|取反运算|||
> > |<<|左移运算|||
> > |>>|右移运算|||
>
> > ##### 成员运算符
> > |运算符|逻辑表达式|描述|实例|
> > |---|---|---|---|
> > |in| x in sequences|如果 x 在 sequences 的序列中找到相符的值，则返回True，否则返回False| 3 in (1, 2, 3) 返回True|
> > |not in| x not in sequences| 如果 x 在 sequences 的序列没有找到相符的值，则返回True，否则返回False| 3 not in (1, 2, 3) 返回 False|
> > 
> > ---
>
>
> > ##### 进制  
> > **1.**  2 进制: 0 和 1，满 2 进 1 ，以0b 或 0B 开头 （ b = binary ）  
> > **2.**  8 进制: 0 - 7，满 8 进 1，以0o 或 0O 开头表示 （ o = octagon ）  
> > **3.**  10 进制: 0 - 9，满 10 进 1  
> > **4.**  16 进制: 0 - 9 [ 10(A) - 15(F) ]，满 16 进 1，以 0x 或 0X 开头表示 （ x = Hexadecagon ），A-F 不区分大小写  
> > 
> > ---
>
> > ##### 二进制转十进制
> > 规则：从最低位（右边）开始算，将每个位上的数提取出来，然后乘以 2 的（ 位数-1 ）次方。
> > ```python
> > # 案例：将 0b1011 转成十进制的数
> > 0b1011 = 
> > 1 * 2 的 (1-1) 次方 = 1
> > 1 * 2 的 (2-1) 次方 = 2
> > 0 * 2 的 (3-1) 次方 = 0
> > 1 * 2 的 (4-1) 次方 = 8
> > 
> > 1 + 2 + 0 + 8 = 11
> > ```
> > ---
> >
> > ##### 八进制转十进制  
> > 规则：从最低位（右边）开始算，将每个位上的数提取出来，然后乘以 8 的（ 位数-1 ）次方。然后求和
> > ```python
> > # 案例：将 0o234 转成十进制的数
> > 0o234 = 
> > 4 * 8^0 = 4
> > 3 * 8^1 = 24
> > 2 * 8^2 = 128
> > 
> > 4 + 24 + 128 = 156
> > ```
> > ---
> >
> > ##### 十六进制转十进制
> > 规则：从最低位（右边）开始算，将每个位上的数提取出来，然后乘以 16 的（ 位数-1 ）次方。然后求和
> > ```python 
> > # 案例：将 0o23A 转成十进制的数
> > 0x23A =
> > 10 * 16^0 = 10
> > 3 * 16^1 = 48
> > 2 * 16^2 = 512
> > 
> > 10 + 48 + 512 = 570
> > ```
> > ---
> > 
>
>> ##### 十进制转二进制
>> ##### 十进制转八进制
>> ##### 十进制转十六进制
>> 
>> ##### 二进制转八进制
>> ##### 二进制转十六进制
>> 
>> ##### 八进制转二进制
>> ##### 十六进制转二进制
