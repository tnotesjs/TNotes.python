# [0019. 函数进阶](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0019.%20%E5%87%BD%E6%95%B0%E8%BF%9B%E9%98%B6)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 什么是递归函数？](#2-什么是递归函数)
- [3. 什么是匿名函数 lambda？](#3-什么是匿名函数-lambda)
- [4. 高阶函数 map、filter、reduce 怎么用？](#4-高阶函数-mapfilterreduce-怎么用)
- [5. 什么是闭包？](#5-什么是闭包)
- [6. 装饰器的原理与实现是怎样的？](#6-装饰器的原理与实现是怎样的)
- [7. 什么是偏函数 functools.partial？](#7-什么是偏函数-functoolspartial)

<!-- endregion:toc -->

## 1. 本节内容

- 递归函数
- 匿名函数（lambda）
- 高阶函数（map、filter、reduce）
- 闭包与自由变量
- 装饰器原理与实现
- 偏函数（functools.partial）

## 2. 什么是递归函数？

递归函数是在函数体内调用自身的函数。每个递归函数都需要一个终止条件（基例）和一个递归步骤。

```python
# 计算阶乘
def factorial(n):
    if n <= 1:      # 基例
        return 1
    return n * factorial(n - 1)  # 递归步骤

print(factorial(5))  # 120

# 斉波那契数列
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))  # 55
```

Python 默认的递归深度限制为 1000 层，可以通过 sys.setrecursionlimit() 修改：

```python
import sys
print(sys.getrecursionlimit())    # 1000
# sys.setrecursionlimit(5000)     # 不建议设置过大
```

递归的优化：使用缓存避免重复计算：

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(100))  # 354224848179261915075（瞬间计算完成）
```

## 3. 什么是匿名函数 lambda？

lambda 是一种小型匿名函数，只能包含一个表达式：

```python
# 语法：lambda 参数: 表达式
add = lambda a, b: a + b
print(add(3, 5))  # 8

# 等价于
def add(a, b):
    return a + b
```

lambda 常用于需要临时函数的场景：

```python
# 排序时指定排序键
students = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
students.sort(key=lambda x: x[1])
print(students)  # [('Charlie', 78), ('Alice', 85), ('Bob', 92)]

# 作为参数传递给高阶函数
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16, 25]
```

## 4. 高阶函数 map、filter、reduce 怎么用？

高阶函数是接受函数作为参数或返回函数的函数。

map() 将函数应用到可迭代对象的每个元素：

```python
numbers = [1, 2, 3, 4, 5]

# 与 lambda 配合
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# 与定义的函数配合
def double(x):
    return x * 2

result = list(map(double, numbers))
print(result)  # [2, 4, 6, 8, 10]

# 多个可迭代对象
result = list(map(lambda a, b: a + b, [1, 2, 3], [10, 20, 30]))
print(result)  # [11, 22, 33]
```

filter() 过滤可迭代对象中的元素：

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# 保留偶数
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8, 10]

# 保留非空字符串
words = ["hello", "", "world", "", "python"]
non_empty = list(filter(None, words))  # None 表示使用元素本身的布尔值
print(non_empty)  # ['hello', 'world', 'python']
```

reduce() 将可迭代对象缩减为单个值：

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# 计算乘积
product = reduce(lambda a, b: a * b, numbers)
print(product)  # 120

# 计算累加和
total = reduce(lambda a, b: a + b, numbers)
print(total)  # 15

# 带初始值
result = reduce(lambda a, b: a + b, numbers, 100)
print(result)  # 115
```

## 5. 什么是闭包？

闭包是一个内层函数引用了外层函数的变量，并且外层函数返回了这个内层函数。这样即使外层函数已经执行完毕，内层函数仍然可以访问那些变量。

```python
def make_multiplier(factor):
    def multiply(x):
        return x * factor  # 引用外层函数的 factor 变量
    return multiply

double = make_multiplier(2)
triple = make_multiplier(3)

print(double(5))   # 10
print(triple(5))   # 15
```

闭包的常见应用：

```python
# 计数器
def make_counter():
    count = 0
    def counter():
        nonlocal count
        count += 1
        return count
    return counter

c = make_counter()
print(c())  # 1
print(c())  # 2
print(c())  # 3

# 延迟计算
def make_power(exponent):
    def power(base):
        return base ** exponent
    return power

square = make_power(2)
cube = make_power(3)
print(square(5))  # 25
print(cube(5))    # 125
```

## 6. 装饰器的原理与实现是怎样的？

装饰器本质上是一个接受函数作为参数并返回新函数的函数。它用于在不修改原函数代码的情况下扩展其功能。

```python
# 基本装饰器
def timer(func):
    import time
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} 执行耗时 {end - start:.4f} 秒")
        return result
    return wrapper

@timer
def slow_function():
    import time
    time.sleep(1)
    return "完成"

result = slow_function()  # slow_function 执行耗时 1.00xx 秒
```

使用 @timer 装饰器等价于：

```python
def slow_function():
    import time
    time.sleep(1)
    return "完成"

slow_function = timer(slow_function)
```

带参数的装饰器：

```python
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def say_hello(name):
    print(f"Hello, {name}!")

say_hello("Alice")
# Hello, Alice!
# Hello, Alice!
# Hello, Alice!
```

保留原函数信息：

```python
from functools import wraps

def my_decorator(func):
    @wraps(func)  # 保留原函数的名称和文档字符串
    def wrapper(*args, **kwargs):
        print("装饰器逻辑")
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def greet(name):
    """打招呼函数"""
    print(f"你好，{name}")

print(greet.__name__)  # greet（而不是 wrapper）
print(greet.__doc__)   # 打招呼函数
```

## 7. 什么是偏函数 functools.partial？

偏函数通过固定函数的部分参数，创建一个新的函数：

```python
from functools import partial

# 固定 base 参数为 2
def power(base, exponent):
    return base ** exponent

square = partial(power, exponent=2)
cube = partial(power, exponent=3)

print(square(5))  # 25
print(cube(5))    # 125

# 实用示例：固定 int() 的 base 参数
int_from_binary = partial(int, base=2)
print(int_from_binary("1010"))  # 10
print(int_from_binary("1111"))  # 15

# 固定 print 的分隔符
print_with_dash = partial(print, sep="-")
print_with_dash("a", "b", "c")  # a-b-c
```
