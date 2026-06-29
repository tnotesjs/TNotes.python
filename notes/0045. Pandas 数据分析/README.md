# [0045. Pandas 数据分析](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0045.%20Pandas%20%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. Series 和 DataFrame 是什么？](#3-series-和-dataframe-是什么)
- [4. 如何读写数据文件？](#4-如何读写数据文件)
- [5. 如何进行数据筛选和操作？](#5-如何进行数据筛选和操作)
- [6. 如何处理缺失值？](#6-如何处理缺失值)

<!-- endregion:toc -->

## 1. 本节内容

- Series 与 DataFrame 数据结构
- 数据的读取与写入（CSV、Excel、数据库）
- 数据清洗与预处理（处理缺失值、重复值）
- 数据的选择、过滤与排序
- 数据分组与聚合（groupby）
- 数据合并与连接（merge、concat）
- 时间序列分析

## 2. 评价

- todo

## 3. Series 和 DataFrame 是什么？

Pandas 的两个核心数据结构：

```python
import pandas as pd

# Series：一维标签数组
s = pd.Series([10, 20, 30], index=["a", "b", "c"])
print(s["b"])  # 20

# DataFrame：二维表格
df = pd.DataFrame({
    "姓名": ["张三", "李四", "王五"],
    "年龄": [25, 30, 28],
    "城市": ["北京", "上海", "广州"],
})
print(df)
#   姓名  年龄  城市
# 0  张三   25  北京
# 1  李四   30  上海
# 2  王五   28  广州

# 基本信息
print(df.shape)    # (3, 3)
print(df.dtypes)   # 各列数据类型
print(df.describe()) # 统计摘要
print(df.info())   # 数据概览
```

## 4. 如何读写数据文件？

::: code-group

```python [读取文件]
import pandas as pd

# 读取 CSV
df = pd.read_csv("data.csv", encoding="utf-8")

# 读取 Excel
df = pd.read_excel("data.xlsx", sheet_name="Sheet1")

# 读取 JSON
df = pd.read_json("data.json")

# 查看前几行
print(df.head())    # 前 5 行
print(df.tail(3))   # 后 3 行
```

```python [保存文件]
import pandas as pd

df = pd.DataFrame({"name": ["Alice"], "age": [25]})

df.to_csv("output.csv", index=False, encoding="utf-8")
df.to_excel("output.xlsx", index=False)
df.to_json("output.json", orient="records", force_ascii=False)
```

:::

## 5. 如何进行数据筛选和操作？

```python
import pandas as pd

df = pd.DataFrame({
    "姓名": ["张三", "李四", "王五", "赵六"],
    "年龄": [25, 30, 28, 35],
    "薪资": [8000, 12000, 10000, 15000],
    "部门": ["技术", "市场", "技术", "市场"],
})

# 列选择
print(df["姓名"])             # 单列
print(df[["姓名", "薪资"]])  # 多列

# 行筛选
print(df[df["年龄"] > 28])       # 条件筛选
print(df.loc[0:1, "姓名":"年龄"])  # 标签索引
print(df.iloc[0:2, 0:2])        # 位置索引

# 排序
print(df.sort_values("薪资", ascending=False))

# 分组统计
print(df.groupby("部门")["薪资"].mean())
print(df.groupby("部门").agg({"u85aa资": ["mean", "max"], "年龄": "mean"}))

# 新增列
df["年薪"] = df["薪资"] * 12

# 删除列
df = df.drop(columns=["年薪"])
```

## 6. 如何处理缺失值？

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "姓名": ["张三", "李四", "王五"],
    "年龄": [25, np.nan, 28],
    "城市": ["北京", "上海", None],
})

# 检查缺失值
print(df.isnull())       # 布尔矩阵
print(df.isnull().sum()) # 每列缺失值数量

# 删除缺失值
df_dropped = df.dropna()           # 删除包含缺失值的行
df_dropped_col = df.dropna(axis=1) # 删除包含缺失值的列

# 填充缺失值
df_filled = df.fillna({"u5e74龄": df["年龄"].mean(), "城市": "未知"})
print(df_filled)
```
