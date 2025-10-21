+++
title = 'Python Integer'
date = 2025-10-19T11:09:09+08:00
draft = false
slug = "4191130"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Integer

这篇用最简单的话，讲清 Python 整数（int）：没有上限、语法好用、但有几个常见坑要注意。

## 一句话认识 int
- `int` 表示整数（…，-2，-1，0，1，2，…）。
- Python 的整数“没有溢出”，可以很大（自动变成大整数）。
- 支持二/八/十六进制字面量：`0b1010`（二进制）、`0o12`（八进制）、`0xA`（十六进制）。
- 数字下划线提高可读性：`1_000_000`。

## 常用操作（够用版）
```python
# 基本算术
a, b = 7, 3
print(a + b, a - b, a * b)  # 10 4 21

# 除法
print(a / b)   # 2.333...  真除（返回 float）
print(a // b)  # 2         地板除（向下取整）
print(a % b)   # 1         取余

# 幂与根
print(2 ** 10)  # 1024

# 同时得到商和余数
print(divmod(7, 3))  # (2, 1)

# 绝对值、幂函数、取整
import math
print(abs(-5))      # 5
print(pow(2, 10))   # 1024（等同 **）
print(math.floor(-2.3))  # -3（向下）
print(math.ceil(-2.3))   # -2（向上）
print(math.trunc(-2.3))  # -2（截断 toward 0）
```

## 进制转换与解析
```python
n = 255
print(bin(n))  # '0b11111111'  二进制字符串
print(oct(n))  # '0o377'       八进制字符串
print(hex(n))  # '0xff'        十六进制字符串

# 按指定进制解析字符串为整数
print(int('1010', 2))  # 10
print(int('ff', 16))   # 255
```

## 字符串格式化（展示更友好）
```python
n = 1234567
print(f'{n:,}')     # '1,234,567'   千分位
print(f'{n:08d}')   # '01234567'    固定宽度，前导 0
print(f'{n:#x}')    # '0x12d687'    十六进制（带前缀）
print(f'{n:b}')     # '100101101011010000111'  二进制
```

## 位运算（处理标志位/掩码）
```python
x = 0b1010
y = 0b0110
print(x & y)   # 0b0010 与
print(x | y)   # 0b1110 或
print(x ^ y)   # 0b1100 异或
print(~x)      # 取反（注意补码）
print(x << 1)  # 左移 1 位（乘以 2）
print(x >> 1)  # 右移 1 位（除以 2 向下）
```

## 与布尔/浮点的关系
```python
True == 1    # True   （bool 是 int 的子类）
False == 0   # True
1 + True     # 2

# 与 float 混算
print(2 + 0.5)   # 2.5（结果变为 float）
print(5 // 2)    # 2   （两个 int 地板除返回 int）
print(5.0 // 2)  # 2.0（涉及 float 时返回 float）
```

## 容易踩雷（简明版）
- `/` 和 `//` 区分：`/` 是真除（返回 float），`//` 是地板除（向下取整）。
- 负数的 `//` 是“向下取整”：`-5 // 2 == -3`，不是 `-2`。
- `bool` 与 `int`：`True == 1`、`False == 0`，写计数/比较时注意可读性。
- 进制解析要用 `int(s, base)`：不要自己写解析；字符串里允许大小写、可带 `0x/0b/0o`。
- 数字字面量不能有多余前导零：`012` 非法（除非是 `0o12` 这样的进制前缀）。
- 位运算和布尔：`True & True == 1`，位运算返回的是 `int`，不是 `True/False`。
- 大整数性能：整数没有上限，但超大数的运算会变慢、占内存多；必要时换算法或近似。
- 身份比较陷阱：小整数可能被驻留，`a is b` 偶尔为真，但请始终用 `==` 比较内容。

## 速查清单
- 基本：`+ - * / // % **`、`divmod(a, b)`、`abs(x)`
- 取整：`math.floor(x)`、`math.ceil(x)`、`math.trunc(x)`
- 进制转换：`bin(n)` / `oct(n)` / `hex(n)`
- 解析：`int(s, base)`（如 `int('ff', 16)`）
- 格式化：`f'{n:,}'`、`f'{n:08d}'`、`f'{n:#x}'`、`f'{n:b}'`
- 位运算：`& | ^ ~ << >>`

## 小示例
```python
# 分支与计数
flags = [True, False, True]
print(sum(flags))  # 2（True 当作 1）

# 地板除与负数
print(7 // 3, -7 // 3)  # 2, -3

# 掩码示例：第 3 位是否为 1
mask = 0b100
value = 0b1011
print(bool(value & mask))  # True

# 十六进制展示
n = 4095
print(hex(n), f'{n:#x}')  # '0xfff', '0xfff'
```