# [0007. 基本语法与数据类型](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0007.%20%E5%9F%BA%E6%9C%AC%E8%AF%AD%E6%B3%95%E4%B8%8E%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. Python 中的标识符和关键字有哪些规则？](#3-python-中的标识符和关键字有哪些规则)
- [4. 变量和常量在 Python 中是如何工作的？](#4-变量和常量在-python-中是如何工作的)
- [5. Python 中如何写注释？](#5-python-中如何写注释)
- [6. 为什么缩进被称为 Python 的灵魂？](#6-为什么缩进被称为-python-的灵魂)
- [7. Python 有哪些基本数据类型？](#7-python-有哪些基本数据类型)
- [8. 字符串如何定义与转义？](#8-字符串如何定义与转义)

<!-- endregion:toc -->

## 1. 本节内容

- 标识符与关键字
- 变量与常量
- 注释的写法
- 缩进规则（Python 的灵魂）
- 基本数据类型（整数、浮点数、布尔值、复数）
- 字符串的定义与转义

## 2. 评价

- todo

## 3. Python 中的标识符和关键字有哪些规则？

标识符是给变量、函数、类等命名的名称。Python 标识符的命名规则：

- 只能由字母（a-z、A-Z）、数字（0-9）和下划线（\_）组成
- 不能以数字开头
- 区分大小写，name 和 Name 是不同的标识符
- 不能使用 Python 的关键字作为标识符

```python
# 合法的标识符
name = "Alice"
_age = 25
student_1 = "Bob"
MAX_SIZE = 100

# 非法的标识符（会报错）
# 1name = "error"    # 不能以数字开头
# my-name = "error"  # 不能包含连字符
# class = "error"    # 不能使用关键字
```

Python 的关键字是语言预留的具有特殊含义的单词，可以通过以下方式查看：

```python
import keyword
print(keyword.kwlist)
# ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await',
#  'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except',
#  'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is',
#  'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return',
#  'try', 'while', 'with', 'yield']
```

命名约定：

- 变量和函数使用小写字母加下划线：my_variable、calculate_sum
- 类名使用大驼峰命名法：MyClass、StudentInfo
- 常量使用全大写加下划线：MAX_SIZE、PI
- 私有变量或方法以下划线开头：\_private_var
- 名称修饰用双下划线开头：\_\_mangled_name

## 4. 变量和常量在 Python 中是如何工作的？

在 Python 中，变量不需要声明类型，赋值时自动确定类型。变量本质上是对象的引用，而不是存储数据的容器。

```python
# 变量赋值
x = 10         # x 引用整数对象 10
name = "Alice" # name 引用字符串对象 "Alice"
pi = 3.14      # pi 引用浮点数对象 3.14

# 动态类型：变量可以随时改变引用的类型
x = 10
x = "hello"    # 现在 x 引用字符串对象
x = [1, 2, 3]  # 现在 x 引用列表对象

# 多个变量同时赋值
a, b, c = 1, 2, 3

# 多个变量赋相同的值
x = y = z = 0
```

Python 中没有真正的常量机制，通常用全大写字母表示常量，这是一种约定而非强制：

```python
PI = 3.14159
MAX_CONNECTIONS = 100
BASE_URL = "https://api.example.com"

# Python 不会阻止你修改"常量"的值
# 但按照约定，不应该修改全大写命名的变量
```

可以使用 type() 函数查看变量的类型：

```python
x = 42
print(type(x))  # <class 'int'>

y = "hello"
print(type(y))  # <class 'str'>
```

## 5. Python 中如何写注释？

注释用于解释代码，不会被解释器执行。Python 支持两种注释方式：

单行注释使用 # 号：

```python
# 这是一个单行注释
x = 10  # 行尾注释

# 可以连续使用多个单行注释
# 来编写多行的注释内容
# 这种方式很常见
```

多行注释使用三引号（虽然严格来说是多行字符串，但常被用作多行注释）：

```python
"""
这是一个多行注释。
可以跨越多行。
通常用于模块、类或函数的文档字符串。
"""

'''
使用单引号的三引号也可以
实现同样的效果。
'''
```

文档字符串（docstring）是一种特殊的注释，放在模块、类或函数的第一行：

```python
def add(a, b):
    """计算两个数的和。

    参数：
        a：第一个数
        b：第二个数

    返回值：
        两个数的和
    """
    return a + b

# 可以通过 __doc__ 属性访问文档字符串
print(add.__doc__)
```

## 6. 为什么缩进被称为 Python 的灵魂？

Python 使用缩进来表示代码块，而不是像 C、Java 等语言使用花括号 {}。缩进是 Python 语法的一部分，错误的缩进会导致程序报错。

```python
# 正确的缩进
if True:
    print("条件成立")
    print("仍在 if 代码块中")
print("不在 if 代码块中")

# 错误的缩进会报 IndentationError
# if True:
# print("缩进不正确")  # IndentationError
```

缩进规则：

- 同一个代码块内的语句必须使用相同的缩进量
- 推荐使用 4 个空格作为一级缩进（PEP 8 规范）
- 不要混合使用 Tab 和空格
- 大多数编辑器可以设置按 Tab 键自动插入 4 个空格

```python
# 多层嵌套缩进
for i in range(3):
    if i > 0:
        for j in range(2):
            print(f"i={i}, j={j}")
```

缩进强制了代码的可读性，使得 Python 代码在视觉上更加整齐统一。

## 7. Python 有哪些基本数据类型？

Python 的基本数据类型包括整数、浮点数、布尔值和复数。

整数（int）：

```python
a = 42
b = -10
c = 0

# Python 的整数没有大小限制
big_num = 99999999999999999999

# 支持不同进制
binary = 0b1010     # 二进制，值为 10
octal = 0o17        # 八进制，值为 15
hexadecimal = 0xFF  # 十六进制，值为 255

# 可以使用下划线分隔大数字，提高可读性
million = 1_000_000
```

浮点数（float）：

```python
pi = 3.14
e = 2.718
negative = -0.5

# 科学计数法
speed_of_light = 3e8      # 3 × 10^8
planck = 6.626e-34         # 6.626 × 10^(-34)

# 浮点数精度问题
print(0.1 + 0.2)  # 0.30000000000000004
# 使用 decimal 模块可以获得精确计算
```

布尔值（bool）：

```python
is_valid = True
is_empty = False

# 布尔值是整数的子类
print(True + True)   # 2
print(True * 10)     # 10
print(int(True))     # 1
print(int(False))    # 0

# 以下值在布尔上下文中被视为 False
# False, 0, 0.0, "", [], (), {}, None
```

复数（complex）：

```python
z = 3 + 4j
print(z.real)  # 3.0（实部）
print(z.imag)  # 4.0（虚部）

z2 = complex(1, 2)  # 创建复数 1+2j
```

## 8. 字符串如何定义与转义？

字符串是 Python 中最常用的数据类型之一，可以使用单引号、双引号或三引号定义。

```python
# 单引号和双引号效果相同
s1 = 'Hello'
s2 = "Hello"

# 字符串中包含引号时可以交替使用
s3 = "It's a book"
s4 = 'He said "hi"'

# 三引号可以定义多行字符串
s5 = """
这是一个
多行字符串
"""

s6 = '''
也可以用
三个单引号
'''
```

转义字符使用反斜杠 \：

```python
# 常用转义字符
print("Hello\nWorld")   # \n 换行
print("Hello\tWorld")   # \t 制表符
print("He said \"hi\"") # \" 双引号
print('It\'s me')       # \' 单引号
print("path\\to\\file") # \\ 反斜杠

# 原始字符串（raw string），忽略转义
path = r"C:\Users\new\test"
print(path)  # C:\Users\new\test
```

字符串是不可变类型，创建后不能修改其中的字符：

```python
s = "hello"
# s[0] = "H"  # TypeError: 'str' object does not support item assignment

# 可以通过创建新字符串来"修改"
s = "H" + s[1:]
print(s)  # Hello
```
