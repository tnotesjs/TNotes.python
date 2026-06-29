# [0044. NumPy 数值计算](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0044.%20NumPy%20%E6%95%B0%E5%80%BC%E8%AE%A1%E7%AE%97)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. 什么是 NumPy 数组？](#3-什么是-numpy-数组)
- [4. NumPy 数组运算怎么用？](#4-numpy-数组运算怎么用)
- [5. 如何进行数组索引和切片？](#5-如何进行数组索引和切片)
- [6. 广播和形状操作是什么？](#6-广播和形状操作是什么)

<!-- endregion:toc -->

## 1. 本节内容

- NumPy 数组的创建与属性
- 数组的索引与切片
- 数组的运算与广播机制
- 通用函数（ufunc）
- 线性代数基础

## 2. 评价

- todo

## 3. 什么是 NumPy 数组？

NumPy 是 Python 科学计算的基础库，核心是多维数组 ndarray：

```python
import numpy as np

# 创建数组
a = np.array([1, 2, 3, 4, 5])
b = np.array([[1, 2, 3], [4, 5, 6]])  # 二维数组

print(a.shape)   # (5,)
print(b.shape)   # (2, 3)
print(b.dtype)   # int64
print(b.ndim)    # 2（维度）

# 常用创建方式
zeros = np.zeros((3, 4))       # 全零数组
ones = np.ones((2, 3))         # 全一数组
rng = np.arange(0, 10, 2)     # [0, 2, 4, 6, 8]
lin = np.linspace(0, 1, 5)    # [0, 0.25, 0.5, 0.75, 1]
rand = np.random.rand(3, 3)   # 随机数组
```

## 4. NumPy 数组运算怎么用？

NumPy 支持向量化运算，比 Python 循环快很多：

```python
import numpy as np

a = np.array([1, 2, 3, 4])
b = np.array([10, 20, 30, 40])

# 算术运算（元素级别）
print(a + b)      # [11 22 33 44]
print(a * b)      # [10 40 90 160]
print(a ** 2)     # [1 4 9 16]
print(np.sqrt(a)) # [1. 1.414 1.732 2.]

# 矩阵运算
m1 = np.array([[1, 2], [3, 4]])
m2 = np.array([[5, 6], [7, 8]])

print(m1 @ m2)          # 矩阵乘法
print(m1.T)             # 转置
print(np.linalg.det(m1)) # 行列式

# 统计函数
data = np.array([85, 92, 78, 95, 88])
print(np.mean(data))   # 平均值：87.6
print(np.std(data))    # 标准差
print(np.max(data))    # 95
print(np.min(data))    # 78
```

## 5. 如何进行数组索引和切片？

```python
import numpy as np

a = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# 基本索引
print(a[0, 1])     # 2（第 0 行第 1 列）
print(a[1])        # [4 5 6]（第 1 行）

# 切片
print(a[0:2, 1:3]) # [[2 3] [5 6]]
print(a[:, 0])     # [1 4 7]（第 0 列）

# 布尔索引
print(a[a > 5])    # [6 7 8 9]

# 花式索引
print(a[[0, 2]])   # [[1 2 3] [7 8 9]]

# 条件赋值
a[a < 3] = 0
print(a)  # [[0 0 3] [4 5 6] [7 8 9]]
```

## 6. 广播和形状操作是什么？

广播（Broadcasting）允许不同形状的数组进行运算：

```python
import numpy as np

# 广播示例
a = np.array([[1, 2, 3], [4, 5, 6]])  # (2, 3)
b = np.array([10, 20, 30])             # (3,)
print(a + b)  # [[11 22 33] [14 25 36]]

# 形状操作
a = np.arange(12)
print(a.reshape(3, 4))   # 重塑为 3x4
print(a.reshape(2, -1))  # 自动计算列数（2x6）

# 拼接
m1 = np.array([[1, 2], [3, 4]])
m2 = np.array([[5, 6], [7, 8]])
print(np.vstack([m1, m2]))  # 垂直拼接
print(np.hstack([m1, m2]))  # 水平拼接
```
