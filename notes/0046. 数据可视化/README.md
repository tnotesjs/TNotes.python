# [0046. 数据可视化](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0046.%20%E6%95%B0%E6%8D%AE%E5%8F%AF%E8%A7%86%E5%8C%96)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 Matplotlib 基础绘图怎么用？](#3--matplotlib-基础绘图怎么用)
- [4. 🤔 Seaborn 绘图怎么用？](#4--seaborn-绘图怎么用)
- [5. 🤔 如何绘制子图和复合图？](#5--如何绘制子图和复合图)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- Matplotlib 基础绘图
- 图形定制（标题、标签、图例、颜色）
- 子图与多图布局
- Seaborn 统计可视化
- Plotly 交互式可视化

## 2. 🫧 评价

- todo

## 3. 🤔 Matplotlib 基础绘图怎么用？

Matplotlib 是 Python 最基础的绘图库：

```python
import matplotlib.pyplot as plt
import numpy as np

# 折线图
x = np.linspace(0, 2 * np.pi, 100)
y = np.sin(x)

plt.figure(figsize=(10, 6))
plt.plot(x, y, label="sin(x)", color="blue", linewidth=2)
plt.plot(x, np.cos(x), label="cos(x)", color="red", linestyle="--")
plt.title("三角函数")
plt.xlabel("x")
plt.ylabel("y")
plt.legend()
plt.grid(True)
plt.savefig("plot.png", dpi=150)
plt.show()
```

常用图表类型：

```python
import matplotlib.pyplot as plt

# 柱状图
categories = ["苹果", "香蕉", "橘子", "葡萄"]
values = [45, 32, 28, 50]
plt.bar(categories, values)
plt.title("水果销量")
plt.show()

# 散点图
import numpy as np
x = np.random.randn(100)
y = np.random.randn(100)
plt.scatter(x, y, alpha=0.5)
plt.title("散点图")
plt.show()

# 饼图
labels = ["Python", "Java", "JavaScript", "C++"]
sizes = [35, 25, 25, 15]
plt.pie(sizes, labels=labels, autopct="%1.1f%%")
plt.title("编程语言占比")
plt.show()
```

## 4. 🤔 Seaborn 绘图怎么用？

Seaborn 是基于 Matplotlib 的统计图表库，提供更美观的默认样式：

```python
import seaborn as sns
import pandas as pd
import matplotlib.pyplot as plt

# 使用内置数据集
tips = sns.load_dataset("tips")

# 分布图
sns.histplot(tips["total_bill"], kde=True)
plt.title("账单金额分布")
plt.show()

# 箱线图
sns.boxplot(x="day", y="total_bill", data=tips)
plt.title("每天的账单分布")
plt.show()

# 热力图
corr = tips[["total_bill", "tip", "size"]].corr()
sns.heatmap(corr, annot=True, cmap="coolwarm")
plt.title("相关性热力图")
plt.show()

# 关系图
sns.pairplot(tips, hue="sex")
plt.show()
```

## 5. 🤔 如何绘制子图和复合图？

```python
import matplotlib.pyplot as plt
import numpy as np

fig, axes = plt.subplots(2, 2, figsize=(12, 8))

# 子图 1：折线图
x = np.linspace(0, 10, 100)
axes[0, 0].plot(x, np.sin(x))
axes[0, 0].set_title("正弦函数")

# 子图 2：柱状图
axes[0, 1].bar(["A", "B", "C"], [30, 50, 20])
axes[0, 1].set_title("柱状图")

# 子图 3：散点图
axes[1, 0].scatter(np.random.randn(50), np.random.randn(50))
axes[1, 0].set_title("散点图")

# 子图 4：直方图
axes[1, 1].hist(np.random.randn(1000), bins=30)
axes[1, 1].set_title("直方图")

plt.tight_layout()
plt.savefig("subplots.png")
plt.show()
```
