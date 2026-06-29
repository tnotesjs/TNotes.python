# [0025. 魔法方法（特殊方法）](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0025.%20%E9%AD%94%E6%B3%95%E6%96%B9%E6%B3%95%EF%BC%88%E7%89%B9%E6%AE%8A%E6%96%B9%E6%B3%95%EF%BC%89)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. **str** 和 **repr** 有什么区别？](#3-str-和-repr-有什么区别)
- [4. 如何重载比较运算符？](#4-如何重载比较运算符)
- [5. 如何重载算术运算符？](#5-如何重载算术运算符)
- [6. 如何让对象支持容器操作？](#6-如何让对象支持容器操作)
- [7. 什么是上下文管理器？](#7-什么是上下文管理器)
- [8. 什么是可调用对象 **call**？](#8-什么是可调用对象-call)

<!-- endregion:toc -->

## 1. 本节内容

- 字符串表示（`__str__`、`__repr__`）
- 比较运算符重载（`__eq__`、`__lt__` 等）
- 算术运算符重载
- 容器模拟（`__getitem__`、`__setitem__`、`__len__`）
- 上下文管理器（`__enter__`、`__exit__`）与 with 语句
- 可调用对象（`__call__`）

## 2. 评价

- todo

## 3. **str** 和 **repr** 有什么区别？

`__str__` 用于用户可读的字符串表示，`__repr__` 用于开发者可读的字符串表示：

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x}, {self.y})"

    def __repr__(self):
        return f"Point({self.x}, {self.y})"

p = Point(3, 4)
print(str(p))    # (3, 4)（调用 __str__）
print(repr(p))   # Point(3, 4)（调用 __repr__）
print(p)         # (3, 4)（print 默认调用 __str__）
```

如果只定义了 `__repr__`，那么 `__str__` 会回退到使用 `__repr__`。建议至少定义 `__repr__`。

## 4. 如何重载比较运算符？

通过实现特殊方法可以让自定义对象支持比较操作：

```python
class Student:
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def __eq__(self, other):
        return self.score == other.score

    def __lt__(self, other):
        return self.score < other.score

    def __le__(self, other):
        return self.score <= other.score

    def __repr__(self):
        return f"Student('{self.name}', {self.score})"

s1 = Student("Alice", 90)
s2 = Student("Bob", 85)
s3 = Student("Charlie", 90)

print(s1 == s3)  # True
print(s1 > s2)   # True
print(s2 < s1)   # True

# 定义了比较方法后可以排序
students = [s1, s2, s3]
students.sort()
print(students)  # [Student('Bob', 85), Student('Alice', 90), Student('Charlie', 90)]
```

可以使用 functools.total_ordering 装饰器减少需要实现的方法数量：

```python
from functools import total_ordering

@total_ordering
class Student:
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def __eq__(self, other):
        return self.score == other.score

    def __lt__(self, other):
        return self.score < other.score
    # 自动生成 __le__、__gt__、__ge__
```

## 5. 如何重载算术运算符？

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)

    def __mul__(self, scalar):
        return Vector(self.x * scalar, self.y * scalar)

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)

print(v1 + v2)  # Vector(4, 6)
print(v1 - v2)  # Vector(-2, -2)
print(v1 * 3)   # Vector(3, 6)
```

常用的算术运算符特殊方法：

- `__add__`：+ 加法
- `__sub__`：- 减法
- `__mul__`：\* 乘法
- `__truediv__`：/ 除法
- `__floordiv__`：// 整除
- `__mod__`：% 取余
- `__pow__`：\*\* 幂运算
- `__neg__`：- 取负（一元运算符）

## 6. 如何让对象支持容器操作？

通过实现容器相关的特殊方法，可以让对象像列表或字典一样使用：

```python
class Playlist:
    def __init__(self):
        self._songs = []

    def add(self, song):
        self._songs.append(song)

    def __len__(self):
        return len(self._songs)

    def __getitem__(self, index):
        return self._songs[index]

    def __setitem__(self, index, value):
        self._songs[index] = value

    def __delitem__(self, index):
        del self._songs[index]

    def __contains__(self, item):
        return item in self._songs

    def __repr__(self):
        return f"Playlist({self._songs})"

pl = Playlist()
pl.add("歌曲A")
pl.add("歌曲B")
pl.add("歌曲C")

print(len(pl))        # 3
print(pl[0])          # 歌曲A
print(pl[1:3])        # ['歌曲B', '歌曲C']
print("歌曲A" in pl)   # True

pl[0] = "新歌曲"
print(pl)  # Playlist(['新歌曲', '歌曲B', '歌曲C'])

# 支持 for 循环遍历（实现了 __getitem__ 就自动支持）
for song in pl:
    print(song)
```

## 7. 什么是上下文管理器？

上下文管理器通过实现 `__enter__` 和 `__exit__` 方法，配合 with 语句使用，确保资源被正确释放：

```python
class DatabaseConnection:
    def __init__(self, db_name):
        self.db_name = db_name

    def __enter__(self):
        print(f"连接数据库：{self.db_name}")
        return self  # 返回值赋给 as 后面的变量

    def __exit__(self, exc_type, exc_val, exc_tb):
        print(f"断开连接：{self.db_name}")
        if exc_type:
            print(f"发生异常：{exc_val}")
        return False  # 返回 True 会压制异常

    def query(self, sql):
        print(f"执行查询：{sql}")

# 使用 with 语句
with DatabaseConnection("mydb") as db:
    db.query("SELECT * FROM users")
# 连接数据库：mydb
# 执行查询：SELECT * FROM users
# 断开连接：mydb
```

也可以使用 contextlib 模块简化上下文管理器的创建：

```python
from contextlib import contextmanager

@contextmanager
def timer():
    import time
    start = time.time()
    yield
    end = time.time()
    print(f"耗时：{end - start:.4f} 秒")

with timer():
    total = sum(range(1000000))
```

## 8. 什么是可调用对象 **call**？

实现了 `__call__` 方法的对象可以像函数一样被调用：

```python
class Adder:
    def __init__(self, n):
        self.n = n

    def __call__(self, x):
        return self.n + x

add5 = Adder(5)
print(add5(3))    # 8
print(add5(10))   # 15

# 检查对象是否可调用
print(callable(add5))  # True
print(callable(42))    # False
```

实用示例：带状态的函数：

```python
class Counter:
    def __init__(self):
        self.count = 0

    def __call__(self):
        self.count += 1
        return self.count

c = Counter()
print(c())  # 1
print(c())  # 2
print(c())  # 3
print(c.count)  # 3
```
