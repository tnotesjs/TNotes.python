# [0013. 元组](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0013.%20%E5%85%83%E7%BB%84)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 如何创建元组？元组的不可变性意味着什么？](#2-如何创建元组元组的不可变性意味着什么)
- [3. 什么是元组拆包？](#3-什么是元组拆包)
- [4. 元组的使用场景有哪些？](#4-元组的使用场景有哪些)

<!-- endregion:toc -->

## 1. 本节内容

- 元组的创建与不可变性
- 元组的拆包（unpacking）
- 元组的使用场景

## 2. 如何创建元组？元组的不可变性意味着什么？

元组（tuple）与列表类似，但是不可变的。一旦创建，就不能修改其中的元素。

```python
# 创建元组
t1 = (1, 2, 3)
t2 = ("apple", "banana", "cherry")
t3 = (1, "hello", 3.14)  # 可以包含不同类型
t4 = ()                  # 空元组

# 单元素元组需要加逗号
t5 = (42,)     # 这是元组
t6 = (42)      # 这是整数，不是元组
print(type(t5)) # <class 'tuple'>
print(type(t6)) # <class 'int'>

# 省略括号也可以创建元组
t7 = 1, 2, 3
print(type(t7)) # <class 'tuple'>

# 使用 tuple() 构造函数
t8 = tuple([1, 2, 3])    # 从列表创建
t9 = tuple("hello")      # ('h', 'e', 'l', 'l', 'o')
```

元组的不可变性意味着不能对元组进行增、删、改操作：

```python
t = (1, 2, 3)
# t[0] = 10      # TypeError: 'tuple' object does not support item assignment
# t.append(4)    # AttributeError: 'tuple' object has no attribute 'append'
# del t[0]       # TypeError: 'tuple' object doesn't support item deletion

# 但可以访问元素
print(t[0])     # 1
print(t[-1])    # 3
print(t[1:3])   # (2, 3)
```

需要注意，如果元组中包含可变对象（如列表），虽然不能替换该元素，但可以修改其内部的内容：

```python
t = (1, [2, 3], 4)
# t[1] = [5, 6]   # TypeError
t[1].append(5)     # 可以修改列表的内容
print(t)           # (1, [2, 3, 5], 4)
```

## 3. 什么是元组拆包？

元组拆包（unpacking）是将元组中的元素分别赋值给多个变量：

```python
# 基本拆包
point = (10, 20)
x, y = point
print(x)  # 10
print(y)  # 20

# 交换两个变量的值
a, b = 1, 2
a, b = b, a
print(a, b)  # 2 1

# 函数返回多个值时实际上返回的是元组
def get_info():
    return "Alice", 25, "Beijing"

name, age, city = get_info()
print(name)  # Alice
```

使用 \* 收集多余的元素：

```python
numbers = (1, 2, 3, 4, 5)
first, *rest = numbers
print(first)  # 1
print(rest)   # [2, 3, 4, 5]（注意返回的是列表）

first, *middle, last = numbers
print(first)   # 1
print(middle)  # [2, 3, 4]
print(last)    # 5

# 忽略不需要的元素
_, _, third = (10, 20, 30)
print(third)  # 30
```

## 4. 元组的使用场景有哪些？

元组在以下场景中非常合适：

作为字典的键：

```python
# 元组可哈希，可以作为字典的键
locations = {}
locations[(40.7128, -74.0060)] = "New York"
locations[(51.5074, -0.1278)] = "London"

# 列表不可哈希，不能作为字典的键
# locations[[40.7128, -74.0060]] = "New York"  # TypeError
```

作为函数的返回值：

```python
def divide(a, b):
    quotient = a // b
    remainder = a % b
    return quotient, remainder  # 返回元组

q, r = divide(17, 5)
print(f"17 除以 5，商为 {q}，余数为 {r}")
```

保护数据不被修改：

```python
# 当你希望数据不被意外修改时，使用元组
DAYS = ("Monday", "Tuesday", "Wednesday", "Thursday",
        "Friday", "Saturday", "Sunday")
STATUS_CODES = (200, 301, 404, 500)
```

存储异构数据：

```python
# 记录一个人的信息
student = ("Alice", 20, "Computer Science")

# 使用命名元组可以更清晰
from collections import namedtuple
Student = namedtuple("Student", ["name", "age", "major"])
s = Student("Alice", 20, "Computer Science")
print(s.name)   # Alice
print(s.age)    # 20
print(s.major)  # Computer Science
```

元组相比列表的优势：

- 元组的创建和访问速度比列表稍快
- 元组占用的内存比列表少
- 元组可以作为字典的键和集合的元素
- 元组的不可变性提供了数据安全保障
