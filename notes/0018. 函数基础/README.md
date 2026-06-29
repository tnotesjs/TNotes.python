# [0018. 函数基础](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0018.%20%E5%87%BD%E6%95%B0%E5%9F%BA%E7%A1%80)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. 如何定义和调用函数？](#3-如何定义和调用函数)
- [4. 函数参数有哪些类型？](#4-函数参数有哪些类型)
- [5. return 语句是如何工作的？](#5-return-语句是如何工作的)
- [6. 变量的作用域是怎样的？](#6-变量的作用域是怎样的)
- [7. 什么是文档字符串 docstring？](#7-什么是文档字符串-docstring)

<!-- endregion:toc -->

## 1. 本节内容

- 函数的定义与调用
- 函数的参数（位置参数、默认参数、关键字参数、可变参数）
- 返回值与 return 语句
- 变量的作用域（全局变量、局部变量）
- 文档字符串（docstring）

## 2. 评价

- todo

## 3. 如何定义和调用函数？

使用 def 关键字定义函数，按函数名加括号调用：

```python
# 定义函数
def greet(name):
    """向指定的人打招呼"""
    print(f"你好，{name}！")

# 调用函数
greet("Alice")   # 你好，Alice！
greet("Bob")     # 你好，Bob！

# 带返回值的函数
def add(a, b):
    return a + b

result = add(3, 5)
print(result)  # 8

# 没有 return 语句的函数默认返回 None
def do_nothing():
    pass

print(do_nothing())  # None
```

## 4. 函数参数有哪些类型？

Python 函数支持多种参数类型：

位置参数：

```python
def power(base, exponent):
    return base ** exponent

print(power(2, 3))  # 8（按位置传参）
```

默认参数：

```python
def greet(name, message="你好"):
    print(f"{message}，{name}！")

greet("Alice")              # 你好，Alice！
greet("Alice", "早安")     # 早安，Alice！
```

关键字参数：

```python
def create_user(name, age, city):
    print(f"{name}，{age} 岁，来自 {city}")

# 使用关键字参数，顺序无关
create_user(age=25, city="Beijing", name="Alice")
```

可变位置参数 \*args：

```python
def total(*args):
    print(type(args))  # <class 'tuple'>
    return sum(args)

print(total(1, 2, 3))       # 6
print(total(1, 2, 3, 4, 5)) # 15
```

可变关键字参数 \*\*kwargs：

```python
def print_info(**kwargs):
    print(type(kwargs))  # <class 'dict'>
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25, city="Beijing")
# name: Alice
# age: 25
# city: Beijing
```

参数组合使用：

```python
def func(a, b, *args, **kwargs):
    print(f"a={a}, b={b}")
    print(f"args={args}")
    print(f"kwargs={kwargs}")

func(1, 2, 3, 4, x=5, y=6)
# a=1, b=2
# args=(3, 4)
# kwargs={'x': 5, 'y': 6}
```

仅关键字参数（\* 之后的参数必须用关键字传递）：

```python
def fetch_data(url, *, timeout=30, retries=3):
    print(f"URL: {url}, timeout={timeout}, retries={retries}")

fetch_data("https://example.com", timeout=10)
# fetch_data("https://example.com", 10)  # TypeError
```

## 5. return 语句是如何工作的？

return 语句用于从函数返回值并结束函数执行：

```python
# 返回单个值
def square(x):
    return x ** 2

# 返回多个值（实际上返回元组）
def divide(a, b):
    return a // b, a % b

quotient, remainder = divide(17, 5)
print(quotient, remainder)  # 3 2

# 提前返回
def find_first_even(numbers):
    for n in numbers:
        if n % 2 == 0:
            return n
    return None  # 没找到时返回 None

result = find_first_even([1, 3, 5, 4, 7])
print(result)  # 4

result = find_first_even([1, 3, 5])
print(result)  # None
```

## 6. 变量的作用域是怎样的？

Python 的变量作用域遵循 LEGB 规则：Local（局部）→ Enclosing（嵌套）→ Global（全局）→ Built-in（内置）。

```python
x = "global"  # 全局变量

def outer():
    x = "enclosing"  # 嵌套作用域变量

    def inner():
        x = "local"  # 局部变量
        print(x)     # local

    inner()
    print(x)  # enclosing

outer()
print(x)  # global
```

使用 global 关键字修改全局变量：

```python
count = 0

def increment():
    global count
    count += 1

increment()
increment()
print(count)  # 2
```

使用 nonlocal 关键字修改嵌套作用域变量：

```python
def counter():
    count = 0

    def increment():
        nonlocal count
        count += 1
        return count

    return increment

c = counter()
print(c())  # 1
print(c())  # 2
print(c())  # 3
```

## 7. 什么是文档字符串 docstring？

文档字符串是放在函数、类或模块第一行的字符串，用于描述其功能。可以通过 `__doc__` 属性或 help() 函数访问。

```python
def calculate_area(radius):
    """计算圆的面积。

    参数：
        radius：圆的半径，必须为正数

    返回值：
        圆的面积

    示例：
        >>> calculate_area(5)
        78.53981633974483
    """
    import math
    return math.pi * radius ** 2

# 查看文档字符串
print(calculate_area.__doc__)
help(calculate_area)
```

常见的 docstring 风格：

::: code-group

```python [Google 风格]
def add(a, b):
    """Add two numbers together.

    Args:
        a: The first number.
        b: The second number.

    Returns:
        The sum of a and b.
    """
    return a + b
```

```python [NumPy 风格]
def add(a, b):
    """Add two numbers together.

    Parameters
    ----------
    a : int or float
        The first number.
    b : int or float
        The second number.

    Returns
    -------
    int or float
        The sum of a and b.
    """
    return a + b
```

:::
