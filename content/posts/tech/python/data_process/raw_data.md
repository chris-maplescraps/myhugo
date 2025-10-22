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
pip install -U pandas numpy scikit-learn pyarrow openpyxl
```

Python 常用导入
```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, MinMaxScaler
```

1) 读写数据
```python
# 读取 CSV / Excel / JSON
df = pd.read_csv('data.csv')
df = pd.read_excel('data.xlsx', sheet_name=0)
df = pd.read_json('data.json')

# 只读取部分列与行
df_small = pd.read_csv('data.csv', usecols=['col1','col2'], nrows=100)

# 保存为 CSV / Parquet（高效）
df.to_csv('clean.csv', index=False)
df.to_parquet('clean.parquet', index=False)
```

2) 快速查看与选择
```python
df.head()        # 前 5 行
df.info()        # 列与类型概览
df.describe()    # 数值列统计

# 选择列 / 条件过滤
sub = df[['col1','col2']]
filtered = df[df['score'] > 80]
filtered = df[(df['score'] > 80) & (df['age'] < 30)]
```

3) 缺失值处理
```python
# 检查缺失
missing = df.isna().sum()

# 删除含缺失的行或列
df_drop_row = df.dropna()          # 行
df_drop_col = df.dropna(axis=1)    # 列

# 填充缺失（均值 / 中位数 / 众数 / 固定值）
df['age'] = df['age'].fillna(df['age'].median())
df['city'] = df['city'].fillna('Unknown')
```

4) 类型与编码
```python
# 类型转换
df['age'] = df['age'].astype('int64')
df['date'] = pd.to_datetime(df['date'])

# 分类编码（one-hot）
df = pd.get_dummies(df, columns=['city'], dtype=int)
```

5) 重复与唯一
```python
# 去重（基于某列或全部列）
df = df.drop_duplicates(subset=['id'])

# 检查唯一值数量
df['city'].nunique()
```

6) 排序与重命名
```python
# 排序
df = df.sort_values(['score','age'], ascending=[False, True])

# 重命名列
df = df.rename(columns={'old_name':'new_name'})
```

7) 列操作与派生特征
```python
# 新列与向量化计算
df['bmi'] = df['weight'] / (df['height']/100)**2

# 条件派生
df['is_adult'] = np.where(df['age'] >= 18, 1, 0)

# 字符串清洗
df['name'] = df['name'].str.strip().str.title()
```

8) 合并与拼接
```python
# 横向合并（按键）
df2 = pd.read_csv('more.csv')
merged = pd.merge(df, df2, on='id', how='left')

# 纵向拼接（堆叠）
stacked = pd.concat([df, df2], axis=0, ignore_index=True)
```

9) 分组与聚合
```python
g = df.groupby('city').agg({'score':'mean','age':'median'}).reset_index()
```

10) 日期与时间
```python
# 解析与提取
df['date'] = pd.to_datetime(df['date'])
df['year'] = df['date'].dt.year
```

11) 归一化 / 标准化（建模前常用）
```python
num_cols = ['age','score']
scaler = StandardScaler()
df[num_cols] = scaler.fit_transform(df[num_cols])
# 或最小-最大归一化
minmax = MinMaxScaler()
df[num_cols] = minmax.fit_transform(df[num_cols])
```

12) 异常值简单处理
```python
# IQR 法（以某列为例）
q1, q3 = df['score'].quantile([0.25, 0.75])
iqr = q3 - q1
low, high = q1 - 1.5*iqr, q3 + 1.5*iqr
clean = df[(df['score'] >= low) & (df['score'] <= high)]
```

13) 切分训练 / 测试集
```python
train, test = train_test_split(df, test_size=0.2, random_state=42)
```

14) 保存清洗结果
```python
clean.to_csv('clean.csv', index=False)
clean.to_parquet('clean.parquet', index=False)
```

小贴士
- 所有操作尽量向量化，少用循环；
- 读写大文件优先使用 Parquet 格式；
- 任何步骤前后都可用 `df.info()` / `df.head()` 快速自检；
- 若涉及时间/地理等专用数据，可补充对应库（如 `geopandas`）。