# [0012. 列表](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0012.%20%E5%88%97%E8%A1%A8)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 如何创建和访问列表？](#2-如何创建和访问列表)
- [3. 列表的增删改查操作有哪些？](#3-列表的增删改查操作有哪些)
- [4. 列表切片与复制有什么区别？](#4-列表切片与复制有什么区别)
- [5. 什么是列表推导式？](#5-什么是列表推导式)
- [6. 列表有哪些常用方法？](#6-列表有哪些常用方法)

<!-- endregion:toc -->

## 1. 本节内容

- 列表的创建与访问
- 列表的增删改查操作
- 列表切片与复制（深拷贝 vs 浅拷贝）
- 列表推导式
- 列表的常用方法

## 2. 如何创建和访问列表？

列表是 Python 中最常用的数据结构，用方括号 [] 定义，可以存储任意类型的元素。

```python
# 创建列表
numbers = [1, 2, 3, 4, 5]
fruits = ["apple", "banana", "cherry"]
mixed = [1, "hello", 3.14, True, None]  # 可以混合类型
empty = []  # 空列表

# 使用 list() 构造函数
nums = list(range(5))      # [0, 1, 2, 3, 4]
chars = list("hello")      # ['h', 'e', 'l', 'l', 'o']

# 通过索引访问元素（从 0 开始）
print(fruits[0])   # apple
print(fruits[1])   # banana
print(fruits[-1])  # cherry（负数索引从末尾开始）
print(fruits[-2])  # banana

# 嵌套列表
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(matrix[0][1])  # 2
print(matrix[1][2])  # 6
```

## 3. 列表的增删改查操作有哪些？

增加元素：

```python
fruits = ["apple", "banana"]

# append() 在末尾添加单个元素
fruits.append("cherry")
print(fruits)  # ['apple', 'banana', 'cherry']

# insert() 在指定位置插入元素
fruits.insert(1, "orange")
print(fruits)  # ['apple', 'orange', 'banana', 'cherry']

# extend() 批量添加元素
fruits.extend(["grape", "mango"])
print(fruits)  # ['apple', 'orange', 'banana', 'cherry', 'grape', 'mango']

# 使用 + 拼接列表（创建新列表）
new_list = [1, 2] + [3, 4]
print(new_list)  # [1, 2, 3, 4]
```

删除元素：

```python
fruits = ["apple", "banana", "cherry", "banana"]

# remove() 删除第一个匹配的元素
fruits.remove("banana")
print(fruits)  # ['apple', 'cherry', 'banana']

# pop() 删除并返回指定位置的元素，默认最后一个
item = fruits.pop()
print(item)    # banana
print(fruits)  # ['apple', 'cherry']

# del 删除指定位置的元素
del fruits[0]
print(fruits)  # ['cherry']

# clear() 清空列表
fruits.clear()
print(fruits)  # []
```

修改元素：

```python
colors = ["red", "green", "blue"]
colors[1] = "yellow"
print(colors)  # ['red', 'yellow', 'blue']

# 通过切片批量修改
colors[0:2] = ["black", "white"]
print(colors)  # ['black', 'white', 'blue']
```

查找元素：

```python
numbers = [10, 20, 30, 40, 50]

# index() 查找元素的索引
print(numbers.index(30))  # 2

# in 判断元素是否存在
print(30 in numbers)   # True
print(60 in numbers)   # False

# count() 统计元素出现次数
nums = [1, 2, 2, 3, 2]
print(nums.count(2))  # 3
```

## 4. 列表切片与复制有什么区别？

列表切片的语法与字符串切片相同：

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(numbers[2:5])     # [2, 3, 4]
print(numbers[:3])      # [0, 1, 2]
print(numbers[7:])      # [7, 8, 9]
print(numbers[::2])     # [0, 2, 4, 6, 8]
print(numbers[::-1])    # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

浅拷贝与深拷贝的区别：

```python
import copy

# 浅拷贝：只复制第一层，嵌套对象仍然共享引用
original = [[1, 2], [3, 4]]
shallow = original.copy()  # 或 original[:] 或 list(original)
shallow[0][0] = 99
print(original)  # [[99, 2], [3, 4]]（原列表也被修改了）

# 深拷贝：完全独立的副本
original = [[1, 2], [3, 4]]
deep = copy.deepcopy(original)
deep[0][0] = 99
print(original)  # [[1, 2], [3, 4]]（原列表不受影响）
```

简单说明：

- 浅拷贝适用于一维列表
- 深拷贝适用于嵌套列表或包含可变对象的列表

## 5. 什么是列表推导式？

列表推导式（List Comprehension）是 Python 中创建列表的简洁写法：

```python
# 基本语法：[表达式 for 变量 in 可迭代对象]
squares = [x ** 2 for x in range(10)]
print(squares)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# 带条件过滤：[表达式 for 变量 in 可迭代对象 if 条件]
evens = [x for x in range(20) if x % 2 == 0]
print(evens)  # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

# 带条件表达式
labels = ["even" if x % 2 == 0 else "odd" for x in range(5)]
print(labels)  # ['even', 'odd', 'even', 'odd', 'even']

# 嵌套循环
pairs = [(x, y) for x in range(3) for y in range(3)]
print(pairs)  # [(0,0), (0,1), (0,2), (1,0), (1,1), (1,2), (2,0), (2,1), (2,2)]

# 展平二维列表
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat = [num for row in matrix for num in row]
print(flat)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

列表推导式通常比普通的 for 循环更简洁，也更快，但不要写得过于复杂，否则会影响可读性。

## 6. 列表有哪些常用方法？

```python
# 排序
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
numbers.sort()               # 原地排序（升序）
print(numbers)               # [1, 1, 2, 3, 4, 5, 6, 9]
numbers.sort(reverse=True)   # 原地排序（降序）
print(numbers)               # [9, 6, 5, 4, 3, 2, 1, 1]

# sorted() 返回新列表，不修改原列表
original = [3, 1, 2]
sorted_list = sorted(original)
print(original)     # [3, 1, 2]（未变）
print(sorted_list)  # [1, 2, 3]

# 自定义排序规则
words = ["banana", "apple", "cherry"]
words.sort(key=len)  # 按长度排序
print(words)  # ['apple', 'banana', 'cherry']

# 反转
numbers = [1, 2, 3, 4, 5]
numbers.reverse()
print(numbers)  # [5, 4, 3, 2, 1]

# 常用内置函数
nums = [3, 1, 4, 1, 5]
print(len(nums))   # 5（长度）
print(max(nums))   # 5（最大值）
print(min(nums))   # 1（最小值）
print(sum(nums))   # 14（求和）
```
