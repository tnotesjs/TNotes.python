# [0016. 迭代器与生成器](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0016.%20%E8%BF%AD%E4%BB%A3%E5%99%A8%E4%B8%8E%E7%94%9F%E6%88%90%E5%99%A8)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. 什么是可迭代对象和迭代器？](#3-什么是可迭代对象和迭代器)
- [4. 如何实现一个自定义迭代器？](#4-如何实现一个自定义迭代器)
- [5. 什么是生成器函数？](#5-什么是生成器函数)
- [6. 什么是生成器表达式？](#6-什么是生成器表达式)
- [7. itertools 模块有哪些常用工具？](#7-itertools-模块有哪些常用工具)

<!-- endregion:toc -->

## 1. 本节内容

- 可迭代对象与迭代器
- 迭代器的实现（`__iter__` 与 `__next__`）
- 生成器函数（`yield`）
- 生成器表达式
- 内置迭代工具（`itertools` 模块）

## 2. 评价

- todo

## 3. 什么是可迭代对象和迭代器？

可迭代对象（Iterable）是可以被 for 循环遍历的对象，如列表、字符串、字典、集合、文件等。迭代器（Iterator）是一个可以记住遍历位置的对象，每次调用 next() 返回下一个元素。

```python
# 可迭代对象
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# 使用 iter() 将可迭代对象转换为迭代器
it = iter(fruits)
print(next(it))  # apple
print(next(it))  # banana
print(next(it))  # cherry
# print(next(it))  # StopIteration 异常
```

判断一个对象是否可迭代：

```python
from collections.abc import Iterable, Iterator

print(isinstance([1, 2, 3], Iterable))  # True
print(isinstance("hello", Iterable))    # True
print(isinstance(123, Iterable))        # False

# 迭代器也是可迭代对象
it = iter([1, 2, 3])
print(isinstance(it, Iterator))  # True
print(isinstance(it, Iterable))  # True
```

for 循环的内部工作机制：

1. 调用 iter() 获取迭代器
2. 反复调用 next() 获取下一个元素
3. 捕获 StopIteration 异常时停止循环

## 4. 如何实现一个自定义迭代器？

自定义迭代器需要实现 `__iter__` 和 `__next__` 两个方法：

```python
class Countdown:
    """倒计时迭代器"""
    def __init__(self, start):
        self.current = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        value = self.current
        self.current -= 1
        return value

# 使用自定义迭代器
for num in Countdown(5):
    print(num)
# 输出：5 4 3 2 1

# 也可以手动调用
c = Countdown(3)
print(next(c))  # 3
print(next(c))  # 2
print(next(c))  # 1
```

另一个示例，生成斐波那契数列：

```python
class Fibonacci:
    def __init__(self, max_count):
        self.max_count = max_count
        self.count = 0
        self.a, self.b = 0, 1

    def __iter__(self):
        return self

    def __next__(self):
        if self.count >= self.max_count:
            raise StopIteration
        value = self.a
        self.a, self.b = self.b, self.a + self.b
        self.count += 1
        return value

for num in Fibonacci(10):
    print(num, end=" ")
# 输出：0 1 1 2 3 5 8 13 21 34
```

## 5. 什么是生成器函数？

生成器函数使用 yield 关键字，每次调用 next() 时从上次 yield 的位置继续执行，这比手动实现迭代器简洁得多：

```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1

# 使用生成器
for num in countdown(5):
    print(num)
# 输出：5 4 3 2 1

# 生成器是惰性的，只在需要时才计算下一个值
gen = countdown(3)
print(next(gen))  # 3
print(next(gen))  # 2
print(next(gen))  # 1
```

生成器的优势是内存效率高，特别适合处理大量数据：

```python
# 读取大文件时使用生成器
def read_large_file(file_path):
    with open(file_path, "r") as f:
        for line in f:
            yield line.strip()

# 生成无限序列
def natural_numbers():
    n = 1
    while True:
        yield n
        n += 1

# 取前 10 个自然数
from itertools import islice
for num in islice(natural_numbers(), 10):
    print(num, end=" ")
# 输出：1 2 3 4 5 6 7 8 9 10
```

yield 和 return 的区别：

- return 终止函数并返回值
- yield 暂停函数并返回值，下次调用 next() 时从暂停处继续执行

## 6. 什么是生成器表达式？

生成器表达式与列表推导式类似，但使用圆括号，返回的是生成器对象而不是列表：

```python
# 列表推导式：立即创建所有元素，占用内存
squares_list = [x ** 2 for x in range(1000000)]

# 生成器表达式：惰性计算，几乎不占用内存
squares_gen = (x ** 2 for x in range(1000000))

print(type(squares_gen))  # <class 'generator'>

# 遍历生成器
for square in squares_gen:
    if square > 20:
        break
    print(square, end=" ")
# 输出：0 1 4 9 16
```

生成器表达式可以直接作为函数参数：

```python
# 求平方和
total = sum(x ** 2 for x in range(10))
print(total)  # 285

# 找出最大值
max_val = max(len(word) for word in ["hello", "world", "python"])
print(max_val)  # 6

# 判断是否所有元素都满足条件
all_positive = all(x > 0 for x in [1, 2, 3, 4])
print(all_positive)  # True
```

## 7. itertools 模块有哪些常用工具？

itertools 是 Python 标准库中的迭代工具模块，提供了许多高效的迭代器工具：

```python
import itertools

# count()  从指定数字开始无限计数
for i in itertools.islice(itertools.count(10, 2), 5):
    print(i, end=" ")
# 输出：10 12 14 16 18

# cycle()  无限循环一个可迭代对象
counter = 0
for color in itertools.cycle(["red", "green", "blue"]):
    print(color, end=" ")
    counter += 1
    if counter >= 6:
        break
# 输出：red green blue red green blue

# repeat()  重复一个值
for item in itertools.repeat("hello", 3):
    print(item, end=" ")
# 输出：hello hello hello
```

组合与排列工具：

```python
import itertools

# chain()  链接多个可迭代对象
for item in itertools.chain([1, 2], [3, 4], [5]):
    print(item, end=" ")
# 输出：1 2 3 4 5

# product()  笛卡尔积
for pair in itertools.product("AB", "12"):
    print(pair, end=" ")
# 输出：('A', '1') ('A', '2') ('B', '1') ('B', '2')

# permutations()  排列
for perm in itertools.permutations("ABC", 2):
    print(perm, end=" ")
# 输出：('A', 'B') ('A', 'C') ('B', 'A') ('B', 'C') ('C', 'A') ('C', 'B')

# combinations()  组合
for comb in itertools.combinations("ABCD", 2):
    print(comb, end=" ")
# 输出：('A', 'B') ('A', 'C') ('A', 'D') ('B', 'C') ('B', 'D') ('C', 'D')
```

分组工具：

```python
import itertools

# groupby()  按键分组（需要先排序）
data = [("fruit", "apple"), ("fruit", "banana"),
        ("veggie", "carrot"), ("veggie", "daikon")]

for key, group in itertools.groupby(data, key=lambda x: x[0]):
    items = [item[1] for item in group]
    print(f"{key}: {items}")
# fruit: ['apple', 'banana']
# veggie: ['carrot', 'daikon']
```
