+++
title = 'Python String'
date = 2025-10-19T11:08:15+08:00
draft = false
slug = "9ffffe8"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# String

##### 🎇 本文总结 Python 字符串（string）的核心知识点、常用技术与高频用法，便于查阅与速记。

## 核心知识点
- 字符串是不可变的序列类型（immutable）；支持索引与切片。
- 字面量：`'...'`、`"..."`、`'''...'''`/`"""..."""`（多行）、`f"..."`（f-string）、`r"..."`（原始字符串）。
- 常见转义：`\n`（换行）、`\t`（制表）、`\\`（反斜杠）、`\'`、`\"`。
- 编码与解码：`str` 使用 Unicode；与 `bytes` 通过 `encode` / `decode` 互转，常用 `utf-8`。
- 判空与 None：空串 `""` 的布尔值为 `False`；`None` 表示“无值”，与空串不同。
- 身份 vs 相等：`==` 比较内容，`is` 比较对象身份；有时小字符串可能驻留，但不要依赖实现细节。

## 创建与不可变性
```python
s = 'hello'
s[0]        # 'h'
# s[0] = 'H'  # TypeError: 字符串不可变
s2 = s + ' world'   # 拼接
s3 = 'ha' * 3       # 重复 -> 'hahaha'
```
- 频繁拼接建议使用列表累积后 `''.join(parts)`，更高效。

## 基本操作
- 索引与切片：`s[i]`、`s[start:end:step]`，支持负索引与省略。
- 成员测试：`'py' in s`、`'java' not in s`。
- 长度：`len(s)`。

## 常用方法（高频）
- 去空白：`s.strip()` / `s.lstrip()` / `s.rstrip()`。
- 分割：`s.split(sep=None, maxsplit=-1)`、按行 `s.splitlines()`。
- 合并：`sep.join(iterable)`（例如：`' '.join(words)`）。
- 查找：`s.find('x')`（未找到返回 -1）、`s.index('x')`（未找到抛异常）。
- 替换：`s.replace(old, new, count=-1)`。
- 大小写：`s.lower()` / `s.upper()` / `s.title()` / `s.capitalize()` / `s.swapcase()`。
- 前后缀：`s.startswith(prefix)` / `s.endswith(suffix)`。
- 判断：`s.isdigit()` / `s.isalpha()` / `s.isalnum()` / `s.isascii()` / `s.isspace()`。
- 对齐/填充：`s.center(width)` / `s.ljust(width)` / `s.rjust(width)` / `s.zfill(width)`。

## 字符串格式化
```python
name, score = 'Alice', 95
f'{name} 得分 {score}'                 # f-string（推荐）
'{0} 得分 {1}'.format(name, score)     # str.format
'%s 得分 %d' % (name, score)           # 旧式 % 格式（不推荐）
```
- f-string 支持表达式与格式说明：`f'{x:.2f}'`、`f'{num:08d}'`。

## 原始字符串与转义
- 原始字符串 `r'...'
` 不处理反斜杠转义，常用于正则：`r"\d+"`。
- 正常字符串中需要写 `"\\"` 表示一个反斜杠。

## 编码与 bytes
```python
s = '你好'
b = s.encode('utf-8')   # bytes
s2 = b.decode('utf-8')  # str
```
- 从文件/网络读取到 `bytes` 时，先按正确编码 `decode` 成 `str`。

## 正则简述（配合字符串处理）
```python
import re
text = 'Order: A-123, B-456'
re.findall(r'[A-Z]-\d+', text)  # ['A-123', 'B-456']
re.sub(r'-\d+', '-XXX', text)   # 'Order: A-XXX, B-XXX'
```
- 简单前后缀匹配尽量用 `startswith`/`endswith`，比正则更快更清晰。

## 性能与技巧
- 构建长字符串：累积到列表，最后 `''.join(parts)`。
- 拼接数字请显式转换或用 f-string：`f'count={n}'`。
- 处理多行文本时，用 `splitlines()` 和 `join` 管理换行。
- 清洗文本：先 `strip()` 再 `split()`，减少意外空项。

## 常用命令速查
- 去空白：`s.strip()`
- 分割：`s.split()` / `s.splitlines()`
- 合并：`' '.join(items)`
- 查找：`s.find('x')` / `s.index('x')`
- 替换：`s.replace('a', 'b')`
- 大小写：`s.lower()` / `s.upper()` / `s.title()`
- 判断：`s.isdigit()` / `s.isalpha()` / `s.isalnum()` / `s.isascii()`
- 对齐/填充：`s.center(10)` / `s.ljust(10)` / `s.rjust(10)` / `s.zfill(5)`
- 前后缀：`s.startswith('pre')` / `s.endswith('suf')`

## 代码示例
```python
s = '  Python String  '
print(len(s))            # 17
print(s.strip())         # 'Python String'
print('Py' in s)         # True
print(s.lower())         # '  python string  '
print(s.replace(' ', '-'))  # '--Python-String--'

parts = ['py', 'thon', '3']
print(''.join(parts))    # 'python3'

name, score = 'Alice', 95
print(f'{name} 得分 {score:.1f}')   # 'Alice 得分 95.0'

text = 'ID: A-12\nID: B-34'
print(text.splitlines())         # ['ID: A-12', 'ID: B-34']
```

