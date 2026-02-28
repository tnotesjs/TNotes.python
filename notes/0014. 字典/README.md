# [0014. 字典](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0014.%20%E5%AD%97%E5%85%B8)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 如何创建和访问字典？](#3--如何创建和访问字典)
- [4. 🤔 字典的增删改查操作有哪些？](#4--字典的增删改查操作有哪些)
- [5. 🤔 如何遍历字典？](#5--如何遍历字典)
- [6. 🤔 什么是字典推导式？](#6--什么是字典推导式)
- [7. 🤔 字典有哪些常用方法？](#7--字典有哪些常用方法)
- [8. 🤔 什么是有序字典 OrderedDict？](#8--什么是有序字典-ordereddict)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- 字典的创建与访问
- 字典的增删改查操作
- 字典的遍历
- 字典推导式
- 字典的常用方法
- 有序字典（collections.OrderedDict）

## 2. 🫧 评价

- todo

## 3. 🤔 如何创建和访问字典？

字典（dict）是 Python 中的键值对数据结构，用花括号 {} 定义：

```python
# 创建字典
person = {"name": "Alice", "age": 25, "city": "Beijing"}
empty = {}  # 空字典

# 使用 dict() 构造函数
person2 = dict(name="Bob", age=30)
print(person2)  # {'name': 'Bob', 'age': 30}

# 从键值对序列创建
pairs = [("a", 1), ("b", 2), ("c", 3)]
d = dict(pairs)
print(d)  # {'a': 1, 'b': 2, 'c': 3}

# 使用 fromkeys() 创建
keys = ["name", "age", "city"]
d = dict.fromkeys(keys, "unknown")
print(d)  # {'name': 'unknown', 'age': 'unknown', 'city': 'unknown'}
```

访问字典的值：

```python
person = {"name": "Alice", "age": 25}

# 通过键访问
print(person["name"])  # Alice
# print(person["email"])  # KeyError：键不存在时报错

# 使用 get() 方法（更安全）
print(person.get("name"))         # Alice
print(person.get("email"))        # None（键不存在返回 None）
print(person.get("email", "N/A")) # N/A（键不存在返回默认值）
```

## 4. 🤔 字典的增删改查操作有哪些？

增加和修改：

```python
person = {"name": "Alice"}

# 直接赋值：键存在则修改，不存在则添加
person["age"] = 25           # 添加
person["name"] = "Bob"       # 修改

# update() 批量更新
person.update({"city": "Beijing", "age": 30})
print(person)  # {'name': 'Bob', 'age': 30, 'city': 'Beijing'}

# setdefault() 键不存在时设置默认值
person.setdefault("email", "unknown@example.com")
print(person["email"])  # unknown@example.com

# 键已存在时 setdefault 不会修改
person.setdefault("name", "Charlie")
print(person["name"])  # Bob（未变）
```

删除：

```python
person = {"name": "Alice", "age": 25, "city": "Beijing"}

# pop() 删除指定键并返回值
age = person.pop("age")
print(age)     # 25
print(person)  # {'name': 'Alice', 'city': 'Beijing'}

# pop() 可以指定默认值，避免 KeyError
result = person.pop("email", "not found")
print(result)  # not found

# popitem() 删除并返回最后一个键值对
item = person.popitem()
print(item)    # ('city', 'Beijing')

# del 删除指定键
person = {"name": "Alice", "age": 25}
del person["age"]
print(person)  # {'name': 'Alice'}

# clear() 清空字典
person.clear()
print(person)  # {}
```

## 5. 🤔 如何遍历字典？

```python
person = {"name": "Alice", "age": 25, "city": "Beijing"}

# 遍历键
for key in person:
    print(key)
# name age city

# 遍历值
for value in person.values():
    print(value)
# Alice 25 Beijing

# 遍历键值对
for key, value in person.items():
    print(f"{key}: {value}")
# name: Alice
# age: 25
# city: Beijing

# 获取所有键、值、键值对
keys = list(person.keys())      # ['name', 'age', 'city']
values = list(person.values())  # ['Alice', 25, 'Beijing']
items = list(person.items())    # [('name', 'Alice'), ('age', 25), ('city', 'Beijing')]
```

## 6. 🤔 什么是字典推导式？

字典推导式允许使用简洁的语法创建字典：

```python
# 基本语法：{key: value for 变量 in 可迭代对象}
squares = {x: x ** 2 for x in range(6)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# 带条件过滤
even_squares = {x: x ** 2 for x in range(10) if x % 2 == 0}
print(even_squares)  # {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}

# 从两个列表创建字典
keys = ["name", "age", "city"]
values = ["Alice", 25, "Beijing"]
person = {k: v for k, v in zip(keys, values)}
print(person)  # {'name': 'Alice', 'age': 25, 'city': 'Beijing'}

# 交换键和值
original = {"a": 1, "b": 2, "c": 3}
reversed_dict = {v: k for k, v in original.items()}
print(reversed_dict)  # {1: 'a', 2: 'b', 3: 'c'}
```

## 7. 🤔 字典有哪些常用方法？

```python
d = {"a": 1, "b": 2, "c": 3}

# copy() 浅拷贝
d2 = d.copy()

# 合并字典（Python 3.9 以上）
d1 = {"a": 1, "b": 2}
d2 = {"b": 3, "c": 4}
merged = d1 | d2
print(merged)  # {'a': 1, 'b': 3, 'c': 4}（d2 的值覆盖 d1）

# 在较旧版本中使用 ** 解包合并
merged = {**d1, **d2}

# 检查键是否存在
print("a" in d)  # True
print("x" in d)  # False

# 获取字典长度
print(len(d))  # 3
```

## 8. 🤔 什么是有序字典 OrderedDict？

在 Python 3.7 以后，普通字典已经保证插入顺序。OrderedDict 是 collections 模块提供的特殊字典，在早期版本中用于保持插入顺序，现在仍有一些独特功能。

```python
from collections import OrderedDict

# 创建 OrderedDict
od = OrderedDict()
od["first"] = 1
od["second"] = 2
od["third"] = 3

# 与普通字典的区别：
# 1. 比较时考虑顺序
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 2, "a": 1}
print(dict1 == dict2)  # True（普通字典不考虑顺序）

od1 = OrderedDict(a=1, b=2)
od2 = OrderedDict(b=2, a=1)
print(od1 == od2)  # False（OrderedDict 考虑顺序）

# 2. move_to_end() 方法
od = OrderedDict(a=1, b=2, c=3)
od.move_to_end("a")        # 移动到末尾
print(list(od.keys()))     # ['b', 'c', 'a']

od.move_to_end("a", last=False)  # 移动到开头
print(list(od.keys()))           # ['a', 'b', 'c']
```

在 Python 3.7 以后，大多数情况下使用普通字典就足够了，只有在需要顺序比较或 move_to_end 等功能时才需要 OrderedDict。
