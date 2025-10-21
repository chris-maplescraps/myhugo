+++
title = 'Python Set'
date = 2025-10-19T11:08:35+08:00
draft = false
slug = "bdb4c68"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Set

这篇用最简单的话，讲清 Python 集合（set）：它是“去重、无序、可变”的元素集合，适合做去重、快速包含判断与集合运算。

## 一句话认识 set
- 特性：元素唯一、无序不可索引、可变（原地增删）。
- 元素必须可哈希（可作为字典键）：数字、字符串、元组可以；列表、字典不行。
- 空集合写法：`set()`（注意 `{}` 是空字典，不是空集合）。
- 不可变集合：`frozenset`（可做字典键）。

## 快速上手
```python
s = {1, 2, 3}
s.add(4)          # {1, 2, 3, 4}
s.update([3, 5])  # {1, 2, 3, 4, 5}（批量加入，自动去重）
s.discard(10)     # 安全删除（不存在也不报错）
s.remove(2)       # 删除（不存在则报错）
s.pop()           # 随机弹出一个元素（无序，不确定是哪一个）
s.clear()         # 清空
```

## 常用命令（方法）
- 添加/批量：`add(x)`、`update(iterable)`
- 删除：`discard(x)`（安全）/ `remove(x)`（严格）/ `pop()`（弹出一个）/ `clear()`
- 查询：`len(s)`、`x in s`、`x not in s`
- 复制：`s.copy()`（浅拷贝）

## 集合运算（高频）
```python
A = {1, 2, 3}
B = {3, 4}
A | B            # 并集 -> {1, 2, 3, 4}
A & B            # 交集 -> {3}
A - B            # 差集 -> {1, 2}
A ^ B            # 对称差 -> {1, 2, 4}

# 对应方法
A.union(B)
A.intersection(B)
A.difference(B)
A.symmetric_difference(B)

# 子集/超集比较
A <= {1,2,3,4}    # True（子集）
A < {1,2,3,4}     # True（真子集）
A.issubset(B)     # 子集判断
A.issuperset(B)   # 超集判断
```

## 去重与快速包含
```python
# 列表去重（不保留原顺序）
unique = list(set([3, 1, 2, 1, 3]))   # [1, 2, 3]（顺序不保证）

# 保序去重（保留出现顺序）
seen = set()
result = []
for x in [3, 1, 2, 1, 3]:
    if x not in seen:
        seen.add(x)
        result.append(x)
# result -> [3, 1, 2]

# 快速包含判断（O(1) 平均）
whitelist = {'alice', 'bob'}
if 'alice' in whitelist:
    pass
```

## 集合推导式（简洁写法）
```python
squares = {x*x for x in range(5)}            # {0, 1, 4, 9, 16}
odd = {x for x in range(10) if x % 2 == 1}   # 过滤保留奇数
```

## 容易踩雷（简明版）
- `{}` 是空字典，不是空集合：空集合请用 `set()`。
- 无序不可索引：不能 `s[0]`；如需顺序，请用 `list` 或 `sorted(s)`。
- `pop()` 弹出任意元素：不要依赖弹出的是某个具体值。
- 元素必须可哈希：`set([1, [2,3]])` 会报错；可改用 `tuple`（如 `set([(1,2)])`）。
- 去重后顺序会丢失：需要保留原顺序时用“保序去重”方案（见上）。
- `update` 和 `add` 区分：`add(x)` 加单个对象；`update(iterable)` 展开加入多个元素。
- `set` 不能存可变对象作为元素（如列表），但可以存不可变集合：`frozenset({...})`。

## 速查清单
- 创建：`set()`、`{...}`、`frozenset(iterable)`
- 添加/批量：`add` / `update`
- 删除：`discard` / `remove` / `pop` / `clear`
- 运算：`| & - ^`、`union`/`intersection`/`difference`/`symmetric_difference`
- 关系：`<= < >= >`、`issubset`/`issuperset`
- 推导式：`{expr for x in iterable if cond}`

## 小示例
```python
A = {1, 2, 3}
B = {3, 4, 5}
print(A | B)      # {1, 2, 3, 4, 5}
print(A & B)      # {3}
print(A - B)      # {1, 2}
print(A ^ B)      # {1, 2, 4, 5}

# 保序去重
items = ['a', 'b', 'a', 'c']
seen, out = set(), []
for x in items:
    if x not in seen:
        seen.add(x)
        out.append(x)
print(out)        # ['a', 'b', 'c']
```