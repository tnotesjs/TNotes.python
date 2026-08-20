# [0015. 集合](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0015.%20%E9%9B%86%E5%90%88)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 如何创建集合？](#2-如何创建集合)
- [3. 集合支持哪些数学运算？](#3-集合支持哪些数学运算)
- [4. 集合有哪些常用方法？](#4-集合有哪些常用方法)
- [5. 什么是集合推导式？](#5-什么是集合推导式)

<!-- endregion:toc -->

## 1. 本节内容

- 集合的创建
- 集合的数学运算（并集、交集、差集、对称差集）
- 集合的常用方法
- 集合推导式

## 2. 如何创建集合？

集合（set）是一个无序、不重复的元素集合，用花括号 {} 或 set() 函数创建：

```python
# 使用花括号创建
fruits = {"apple", "banana", "cherry"}
print(fruits)  # {'cherry', 'banana', 'apple'}（顺序可能不同）

# 重复元素会被自动去除
numbers = {1, 2, 2, 3, 3, 3}
print(numbers)  # {1, 2, 3}

# 使用 set() 构造函数
s1 = set([1, 2, 3, 2, 1])    # 从列表创建，{1, 2, 3}
s2 = set("hello")             # 从字符串创建，{'h', 'e', 'l', 'o'}
s3 = set()                    # 空集合（注意：{} 创建的是空字典）

# 集合的元素必须是可哈希的（不可变类型）
# {[1, 2]}  # TypeError：列表不可哈希
valid_set = {1, "hello", (1, 2)}  # 整数、字符串、元组都可以
```

集合的基本操作：

```python
s = {1, 2, 3}

# 添加元素
s.add(4)
print(s)  # {1, 2, 3, 4}

# 批量添加
s.update([5, 6, 7])
print(s)  # {1, 2, 3, 4, 5, 6, 7}

# 删除元素
s.remove(7)     # 元素不存在时报 KeyError
s.discard(10)   # 元素不存在时不报错
item = s.pop()  # 随机删除并返回一个元素

# 检查元素是否存在
print(3 in s)   # True
print(10 in s)  # False

# 获取集合长度
print(len(s))
```

## 3. 集合支持哪些数学运算？

集合支持并集、交集、差集、对称差集等数学运算：

```python
a = {1, 2, 3, 4, 5}
b = {4, 5, 6, 7, 8}

# 并集：两个集合的所有元素
print(a | b)          # {1, 2, 3, 4, 5, 6, 7, 8}
print(a.union(b))     # {1, 2, 3, 4, 5, 6, 7, 8}

# 交集：两个集合共有的元素
print(a & b)               # {4, 5}
print(a.intersection(b))   # {4, 5}

# 差集：在 a 中但不在 b 中的元素
print(a - b)              # {1, 2, 3}
print(a.difference(b))    # {1, 2, 3}

# 对称差集：不同时属于两个集合的元素
print(a ^ b)                       # {1, 2, 3, 6, 7, 8}
print(a.symmetric_difference(b))   # {1, 2, 3, 6, 7, 8}
```

集合的关系判断：

```python
a = {1, 2, 3}
b = {1, 2, 3, 4, 5}
c = {1, 2, 3}

# 子集判断
print(a <= b)            # True（a 是 b 的子集）
print(a.issubset(b))     # True

# 超集判断
print(b >= a)              # True（b 是 a 的超集）
print(b.issuperset(a))     # True

# 相等判断
print(a == c)  # True

# 不相交判断
d = {6, 7, 8}
print(a.isdisjoint(d))  # True（没有共同元素）
```

集合的一个典型应用是去重：

```python
numbers = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
unique = list(set(numbers))
print(unique)  # [1, 2, 3, 4]（顺序可能不同）
```

## 4. 集合有哪些常用方法？

```python
s = {1, 2, 3, 4, 5}

# 复制
s2 = s.copy()

# 清空
s2.clear()

# frozenset：不可变集合
fs = frozenset([1, 2, 3])
# fs.add(4)  # AttributeError：frozenset 没有 add 方法

# frozenset 可以作为字典的键或集合的元素
d = {frozenset([1, 2]): "pair"}
print(d[frozenset([1, 2])])  # pair
```

## 5. 什么是集合推导式？

集合推导式与列表推导式类似，使用花括号：

```python
# 基本语法
squares = {x ** 2 for x in range(10)}
print(squares)  # {0, 1, 4, 9, 16, 25, 36, 49, 64, 81}

# 带条件过滤
even_squares = {x ** 2 for x in range(10) if x % 2 == 0}
print(even_squares)  # {0, 4, 16, 36, 64}

# 从字符串提取唯一字符
text = "hello world"
unique_chars = {c for c in text if c != " "}
print(unique_chars)  # {'h', 'e', 'l', 'o', 'w', 'r', 'd'}
```
