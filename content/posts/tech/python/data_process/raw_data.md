+++
title = 'Raw_data'
date = 2025-10-22T21:30:55+08:00
draft = true
slug = "ee07051"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Raw_data

## 技术背景

下面是一份使用 Python 进行数据预处理的常用操作速查，示例简洁易懂、可直接复制使用。

提示：建议安装依赖后，在任意脚本或交互环境中运行。

终端安装依赖
```
# 安装/升级常用数据处理库
pip install -U pandas numpy pyarrow openpyxl  # 安装并升级到最新版本
```

Python 常用导入
```python
import pandas as pd  # 导入 pandas 并使用 pd 作为简写
import numpy as np   # 导入 numpy 并使用 np 作为简写
```

1) 读写数据
```python
# 读取 CSV / Excel / JSON
df = pd.read_csv('data.csv')  # 从 CSV 文件读取为 DataFrame
df = pd.read_excel('data.xlsx', sheet_name=0)  # 读取 Excel 第一个工作表
df = pd.read_json('data.json')  # 从 JSON 文件读取为 DataFrame

# 只读取部分列与行
df_small = pd.read_csv('data.csv', usecols=['col1','col2'], nrows=100)  # 选择列并限制行数

# 保存为 CSV / Parquet（高效）
df.to_csv('clean.csv', index=False)  # 保存为 CSV，去除行索引
df.to_parquet('clean.parquet', index=False)  # 保存为 Parquet，适合大数据
```

2) 快速查看与选择
```python
df.head()        # 前 5 行
df.info()        # 列与类型概览
df.describe()    # 数值列统计

# 选择列 / 条件过滤
sub = df[['col1','col2']]  # 选取指定列
filtered = df[df['score'] > 80]  # 过滤分数大于 80 的行
filtered = df[(df['score'] > 80) & (df['age'] < 30)]  # 复合条件筛选
```

3) 缺失值处理
```python
# 检查缺失
missing = df.isna().sum()  # 统计每列缺失值数量

# 删除含缺失的行或列
df_drop_row = df.dropna()          # 删除包含缺失值的行
df_drop_col = df.dropna(axis=1)    # 删除包含缺失值的列

# 填充缺失（均值 / 中位数 / 众数 / 固定值）
df['age'] = df['age'].fillna(df['age'].median())  # 用中位数填充年龄缺失
df['city'] = df['city'].fillna('Unknown')  # 用固定值填充城市缺失
```

4) 类型与编码
```python
# 类型转换
df['age'] = df['age'].astype('int64')  # 将年龄列转换为整数类型
df['date'] = pd.to_datetime(df['date'])  # 将日期列转换为日期时间类型

# 分类编码（one-hot）
df = pd.get_dummies(df, columns=['city'], dtype=int)  # 对城市列做 one-hot 编码
```

5) 重复与唯一
```python
# 去重（基于某列或全部列）
df = df.drop_duplicates(subset=['id'])  # 根据 id 去重

# 检查唯一值数量
df['city'].nunique()  # 统计城市列的唯一值数量
```

6) 排序与重命名
```python
# 排序
df = df.sort_values(['score','age'], ascending=[False, True])  # 先按分数降序，再按年龄升序

# 重命名列
df = df.rename(columns={'old_name':'new_name'})  # 重命名列
```

7) 列操作与派生特征
```python
# 新列与向量化计算
df['bmi'] = df['weight'] / (df['height']/100)**2  # 计算 BMI 指标

# 条件派生
df['is_adult'] = np.where(df['age'] >= 18, 1, 0)  # 年龄≥18 记为成人

# 字符串清洗
df['name'] = df['name'].str.strip().str.title()  # 去空格并将每个词首字母大写
```

8) 合并与拼接
```python
# 横向合并（按键）
df2 = pd.read_csv('more.csv')  # 读取补充数据
merged = pd.merge(df, df2, on='id', how='left')  # 按 id 左连接合并

# 纵向拼接（堆叠）
stacked = pd.concat([df, df2], axis=0, ignore_index=True)  # 纵向堆叠并重排索引
```

9) 分组与聚合
```python
g = df.groupby('city').agg({'score':'mean','age':'median'}).reset_index()  # 按城市统计分数均值与年龄中位数
```

10) 日期与时间
```python
# 解析与提取
df['date'] = pd.to_datetime(df['date'])  # 解析为日期时间
df['year'] = df['date'].dt.year  # 提取年份
```



12) 异常值简单处理
```python
# IQR 法（以某列为例）
q1, q3 = df['score'].quantile([0.25, 0.75])  # 计算 25% 与 75% 分位数
iqr = q3 - q1  # 四分位距
low, high = q1 - 1.5*iqr, q3 + 1.5*iqr  # IQR 范围外的阈值
clean = df[(df['score'] >= low) & (df['score'] <= high)]  # 过滤掉异常值
```



14) 保存清洗结果
```python
clean.to_csv('clean.csv', index=False)  # 保存清洗后数据为 CSV
clean.to_parquet('clean.parquet', index=False)  # 保存为 Parquet 格式
```

小贴士
- 所有操作尽量向量化，少用循环；
- 读写大文件优先使用 Parquet 格式；
- 任何步骤前后都可用 `df.info()` / `df.head()` 快速自检；
- 若涉及时间/地理等专用数据，可补充对应库（如 `geopandas`）。