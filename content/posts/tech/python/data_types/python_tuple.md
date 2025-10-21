+++
title = 'Python Tuple'
date = 2025-10-19T11:08:40+08:00
draft = false
slug = "2340053"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Tuple

这篇用最简单的话，讲清 Python 元组（tuple）：它是“有序、不可变、可重复”的序列，适合表示固定不变的数据、函数多返回值、字典键等场景。

## 一句话认识 tuple
- 特性：有序、不可变（不能增删改）、允许重复、可嵌套。
- 单个元素的元组要加逗号：`(3,)`；`(3)` 只是数字 3。
- 逗号才是“元组生成符”，括号常用于可读性或解包。
- 元素可哈希时，`tuple` 本身可哈希，可做字典键。

## 快速上手
```python
# 创建
empty = ()
a = (1, 2, 3)
b = 1, 2, 3            # 不写括号也行（逗号决定是 tuple）
single = (42,)         # 单元素一定要逗号

# 访问与切片（返回新 tuple）
a[0]        # 1
a[-1]       # 3
a[1:3]      # (2, 3)

# 解包与多返回值
x, y = (10, 20)
print(x, y)            # 10 20

# 交换变量（常见技巧）
a, b = b, a

# 方法（只有两个）：
a.count(2)             # 统计 2 的出现次数
a.index(3)             # 返回 3 的首个索引

# 成员与长度
2 in a                 # True
len(a)                 # 3
```

## 常用命令（函数/方法）
- 转换：`tuple(iterable)`、`list(t)`、`str(t)`、`sorted(t)`（返回列表）
- 组合：`a + b`（拼接）、`a * n`（重复）
- 枚举/打包：`enumerate(iterable)`、`zip(a, b)`（返回由元组构成的迭代器）
- 方法：`t.count(x)`、`t.index(x)`

## 典型应用场景
- 多返回值/解包：函数返回多个值，外部一行解包。
- 字典键/集合元素：不可变且可哈希（元素也需可哈希）时可用作键。
- 常量表：选择用 `tuple` 而非 `list` 明确“不该被修改”。

## 与 list 的对比（一屏看懂）
- 可变性：`list` 可变；`tuple` 不可变（更安全）。
- 语义：`tuple` 表达“固定组合”；`list` 表达“可变集合”。
- 内存/性能：`tuple` 通常更省内存、创建更快；大量改动用 `list` 更合适。

## 容易踩雷
- 单元素逗号：`(3,)` 才是单元素元组；`(3)` 只是括号。
- 不可变≠完全不变：若内含可变对象，内部内容仍可变。
  ```python
  t = ([1, 2], 3)
  t[0].append(9)     # 合法：修改列表，不是修改元组结构
  # t[0] = [1,2,3]  # 非法：试图替换元组的元素
  ```
- `sorted(tuple)` 返回列表：如需元组可再 `tuple(sorted(t))`。
- 切片返回新元组：不会影响原数据。
- 做字典键：只有当所有元素都可哈希时才行。
- 运算优先级：逗号比加法低；需要用括号确保你得到的是期望的元组。

## 速查清单
- 创建：`()`, `(a, b)`, `(x,)`, `a, b`（逗号决定是元组）
- 访问：`t[i]`, `t[a:b]`
- 方法：`count`、`index`
- 运算：`+` 拼接、`*` 重复、`in` 成员、`len`
- 转换：`tuple(iter)`, `list(t)`, `sorted(t)`
- 解包：`a, b = t`、`a, *rest = t`

## 小示例
```python
# 1) 多返回值
def stats(nums):
    return min(nums), max(nums), sum(nums)/len(nums)
lo, hi, avg = stats([2, 5, 9])
print(lo, hi, avg)

# 2) 作为字典键（坐标）
points = {(0, 0): 'origin', (1, 2): 'p1'}
print(points[(1, 2)])

# 3) 与 namedtuple（可读性更强）
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(3, 4)
print(p.x, p.y)      # 3 4
# namedtuple 仍不可变，且可哈希（字段均可哈希时）
```