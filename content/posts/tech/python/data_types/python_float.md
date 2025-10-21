+++
title = 'Python Float'
date = 2025-10-19T11:09:14+08:00
draft = false
slug = "86b4563"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Float

这篇用最简单的话，讲清 Python 浮点数（float）：它用来表示带小数的数字，但不是所有小数都能“精确”表示，因此比较和计算要有正确姿势。

## 一句话认识 float
- `float` 是带小数的数字类型，比如 `1.5`、`0.1`。
- 不是所有十进制小数都能精确表示（比如 `0.1`），所以有“微小误差”。
- 有三个特殊值：`inf`（正无穷）、`-inf`（负无穷）、`nan`（不是一个数）。

## 为什么 0.1 + 0.2 不等于 0.3？
- 因为 `0.1` 和 `0.2` 在二进制里是“无限循环”的近似数，计算后会带一点点误差。
```python
0.1 + 0.2 == 0.3   # False
```
- 正确比较方式：用“差不多就算相等”的判断。
```python
import math
math.isclose(0.1 + 0.2, 0.3, rel_tol=1e-9, abs_tol=0.0)  # True
```

## 常用操作（够用版）
- 四舍五入（注意：Python 的 `round` 是“银行家舍入”，.5 会向偶数靠拢）：
```python
round(2.5)  # 2
round(3.5)  # 4
round(1.2345, 2)  # 1.23
```
- 特殊值判断：
```python
import math
math.isfinite(x)  # x 是否有限（不是 inf/-inf/nan）
math.isinf(x)     # 是否无穷
math.isnan(x)     # 是否 NaN（不是一个数）
```
- 格式化输出（控制显示样式）：
```python
n = 1234.56789
f"{n:.2f}"         # '1234.57'  保留两位小数
f"{n:e}"           # '1.234568e+03' 科学计数法
format(n, ",.2f")  # '1,234.57'  千分位
```

## 计算里的小技巧
- 大量求和更稳：
```python
import math
math.fsum([1e100, 1, -1e100])  # 比 sum 更稳定
```
- 比较相等尽量用近似：
```python
math.isclose(a, b, rel_tol=1e-9, abs_tol=1e-12)
```

## Decimal（金额等需要“真的精确”）
- 如果场景需要十进制“严格精确”（比如金额），用 `decimal.Decimal`。
- 关键点：从“字符串”创建，别直接把 `float` 丢进去。
```python
from decimal import Decimal, ROUND_HALF_UP
Decimal('0.1') + Decimal('0.2') == Decimal('0.3')  # True（精确）
Decimal(0.1)  # 不精确（带入了 float 的误差）

# 金额常用四舍五入
amount = Decimal('2.345')
amount.quantize(Decimal('0.01'), rounding=ROUND_HALF_UP)  # 2.35
```

## Fraction（分数要精确）
- 需要精确分数计算时用 `fractions.Fraction`。
```python
from fractions import Fraction
Fraction(1, 3) + Fraction(1, 6)  # Fraction(1, 2)
```

## 容易踩雷（简明版）
- `0.1 + 0.2 != 0.3`：用 `math.isclose` 比较。
- `round` 的 .5 不是总向上：是“银行家舍入”（向偶数）。
- `Decimal` 要用字符串创建：`Decimal('1.23')`，不要 `Decimal(1.23)`。
- `nan` 的比较永远不相等：用 `math.isnan(x)` 判断。
- 文本转浮点要先清洗：`float('1,234.5')` 会报错（逗号）。
- 负零展示问题：`-0.0 == 0.0`，但显示可能带“-”，格式化时留意。
- `Decimal` 和 `float` 不要混着算：会退化为 `float`，丢精度。

## 速查清单
- 近似比较：`math.isclose(a, b, rel_tol=1e-9, abs_tol=0.0)`
- 判断状态：`math.isfinite(x)` / `math.isinf(x)` / `math.isnan(x)`
- 稳定求和：`math.fsum(iterable)`
- 四舍五入：`round(x, n)`（.5 向偶数）
- 格式化：`f"{x:.2f}"`、`f"{x:e}"`、`format(x, ',.2f')`
- 精确金额：`Decimal('...')` + `quantize(..., ROUND_HALF_UP)`

## 小示例
```python
import math
print(math.isclose(0.1 + 0.2, 0.3))  # True

# 金额四舍五入
from decimal import Decimal, ROUND_HALF_UP
print(Decimal('2.345').quantize(Decimal('0.01'), rounding=ROUND_HALF_UP))  # 2.35

# 显示两位小数
x = 12345.6789
print(f"{x:.2f}")     # 12345.68
print(format(x, ",.2f"))  # 12,345.68
```