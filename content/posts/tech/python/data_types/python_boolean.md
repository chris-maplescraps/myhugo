+++
title = 'Python Boolean'
date = 2025-10-19T11:08:49+08:00
draft = false
slug = "3495985"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Boolean

本文总结 Python 布尔（Boolean）类型的核心知识点、常用技术与高频用法，并梳理常见坑位与避免策略。

## 核心知识点
- 类型与取值：`bool` 只有两个值：`True` 与 `False`，二者为单例。
- 继承关系：`bool` 是 `int` 的子类；`True == 1`、`False == 0`，参与算术运算会当作 1/0。
- 真值判定（Truthiness）：`if x:` 实际调用 `bool(x)`；对象可通过实现 `__bool__` 或 `__len__` 决定其真值。
- 逻辑运算符：`not`、`and`、`or`，具有短路特性与固定优先级（`not` > `and` > `or`）。
- 比较运算：比较表达式返回布尔；支持链式比较（如 `0 < x < 10`）。
- 单例比较：与 `None` 比较使用 `is` / `is not`，不要用 `==`。

## 真值规则与常见假值
- 假值（`bool(x) is False`）常见成员：`False`、`None`、数值零（`0`、`0.0`、`0j`、`Decimal(0)`、`Fraction(0, 1)`）、空容器（`''`、`[]`、`{}`、`set()`、`range(0)`）。
- 真值但易误解：`float('nan')`、`Decimal('NaN')` 的布尔值为 `True`（容易误判为空/无效）。
- 非零整数（包括负数）都为 `True`；非空字符串（例如 `'0'`、`'False'`）也为 `True`。

## 逻辑运算与短路
```python
# 优先级：not > and > or
not True         # False
True and False   # False
True or False    # True

# 短路：左侧确定结果时，右侧不再求值
expr and f()     # expr 为 False 时，f() 不执行
expr or g()      # expr 为 True 时，g() 不执行

# and/or 返回“操作数”本身（非强制转 bool）
0 or 'default'   # 'default'
'a' and 123      # 123
'' and 123       # ''
```
- 模式：`value = x or default` 常用于提供默认值；若 `x` 可能为合法的假值（如 `0`），请改用显式判断。

## 比较与链式比较
```python
x = 5
0 < x < 10          # True，等价于 (0 < x) and (x < 10)
1 == True           # True；但不建议依赖这种语义写业务逻辑
None == False       # False；与 None 比较用 is/is not
```
- 推荐：区间判断使用链式比较可读性更好。

## 类型转换与常用函数
```python
bool(0)           # False
bool('')          # False
bool('False')     # True（非空字符串）
int(True)         # 1
int(False)        # 0

any([True, False, False])  # True（存在任何真值）
all([True, 1, 'x'])        # True（所有元素真值为真）
any([])                    # False
all([])                    # True（约定：空集的全称命题为真）
```
- 解析字符串为布尔：不要直接 `bool(s)`；请用自定义白名单映射（如 `{'1','true','yes','on'}`）或第三方库。

## 容器与对象的真值
- 容器空则为 `False`，非空为 `True`：`if items:` 判断是否有元素。
- 自定义对象可实现：
```python
class Box:
    def __init__(self, items):
        self.items = items
    def __bool__(self):
        return bool(self.items)   # 依赖内容是否为空
```

## 数值关系与统计
```python
True + True       # 2
sum([True, False, True])   # 2，统计条件成立次数的简便方式
min(True, False)  # False
max(True, False)  # True
```
- 推荐：在计数场景中以 `sum(cond for ...)` 统计满足条件的数量，简洁高效。

## 与 NumPy/Pandas 的注意事项
- `and`/`or` 不能用于数组/Series 的按元素逻辑运算（会抛错或产生意外）。
- 使用按位运算符：`&`（与）、`|`（或）、`~`（非），并加括号：
```python
import numpy as np
import pandas as pd
s = pd.Series([1, 2, 3])
mask = (s > 1) & (s < 3)   # 正确
# (s > 1) and (s < 3)      # 错误：ValueError
```
- 聚合判断：`arr.any()` / `arr.all()`，或 `cond.any()` / `cond.all()`。

## 容易踩雷
- `bool` 是 `int` 子类：`True == 1`、`False == 0`；避免将布尔与整数混用影响可读性。
- `bool('False') is True`：解析字符串为布尔需自定义映射，不要用 `bool(s)`。
- `and`/`or` 返回操作数本身：`a or b` 不一定是 `True/False`，而是 `a` 或 `b`；写条件表达式时留意此语义。
- NaN 的布尔为 `True`：`float('nan')`、`Decimal('NaN')` 不是“空”，判断缺失要用 `math.isnan`/`pd.isna`。
- 与 `None` 比较用 `is`：`x is None` / `x is not None`，不要用 `==`。
- 数组/Series 使用 `&`/`|`：不要用 `and`/`or` 进行按元素逻辑。
- 默认值模式陷阱：`x or default` 会把合法的假值（如 `0`、`''`）替换掉，需改用显式判断：
```python
value = x if x is not None else default
```

## 常用速查
- 逻辑运算：`not a`、`a and b`、`a or b`
- 真值判断：`if x:` / `if not x:`
- 链式比较：`low < x <= high`
- 单例比较：`x is None` / `x is not None`
- 统计布尔：`sum(flags)`、`any(iterable)`、`all(iterable)`
- 数组逻辑：`(cond1 & cond2) | cond3`，聚合用 `.any()` / `.all()`

## 示例
```python
# 典型条件写法
text = 'hello'
if text:                 # 非空即真
    print('has text')

# 默认值提供
port = 0
visible_port = port or 8080    # 小心：这里会得到 8080
visible_port = port if port != 0 else 8080  # 更稳妥

# 计数满足条件的元素
nums = [0, 1, 2, 3]
count = sum(n % 2 == 0 for n in nums)  # 偶数个数：2

# None 判断
result = None
if result is None:
    print('no result')

# 链式比较与短路
x = 5
if 0 < x < 10 and (x % 2 == 1):
    print('ok')
```