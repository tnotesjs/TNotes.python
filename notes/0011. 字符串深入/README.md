# [0011. 字符串深入](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0011.%20%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%B7%B1%E5%85%A5)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. Python 有哪些字符串格式化方式？](#3-python-有哪些字符串格式化方式)
- [4. 字符串有哪些常用方法？](#4-字符串有哪些常用方法)
- [5. 字符串的切片操作怎么用？](#5-字符串的切片操作怎么用)
- [6. 字符串的编码与解码是怎么回事？](#6-字符串的编码与解码是怎么回事)

<!-- endregion:toc -->

## 1. 本节内容

- 字符串的格式化（%、format()、f-string）
- 字符串的常用方法（split、join、strip、replace 等）
- 字符串的切片操作
- 字符串编码与解码（encode、decode）

## 2. 评价

- todo

## 3. Python 有哪些字符串格式化方式？

Python 提供了三种主要的字符串格式化方式：

% 格式化（老式写法）：

```python
name = "Alice"
age = 25
print("我叫 %s，今年 %d 岁" % (name, age))
# 我叫 Alice，今年 25 岁

# 常用占位符
# %s 字符串
# %d 整数
# %f 浮点数
# %x 十六进制
pi = 3.14159
print("圆周率约为 %.2f" % pi)  # 圆周率约为 3.14
```

format() 方法：

```python
name = "Bob"
age = 30

# 位置参数
print("我叫 {}，今年 {} 岁".format(name, age))

# 索引参数
print("我叫 {0}，今年 {1} 岁，我是 {0}".format(name, age))

# 命名参数
print("我叫 {n}，今年 {a} 岁".format(n=name, a=age))

# 格式指定
pi = 3.14159
print("圆周率：{:.2f}".format(pi))  # 圆周率：3.14
print("{:>10}".format("right"))   #      right（右对齐，宽度 10）
print("{:<10}".format("left"))    # left      （左对齐）
print("{:^10}".format("center"))  #   center  （居中）
```

f-string（Python 3.6 以上，推荐使用）：

```python
name = "Charlie"
age = 35

# 基本用法
print(f"我叫 {name}，今年 {age} 岁")

# 支持表达式
print(f"2 + 3 = {2 + 3}")
print(f"大写：{name.upper()}")

# 格式指定
pi = 3.14159
print(f"圆周率：{pi:.2f}")  # 圆周率：3.14

# 填充与对齐
print(f"{'hello':>10}")   #      hello
print(f"{'hello':<10}")   # hello
print(f"{'hello':^10}")   #   hello

# 千位分隔符
num = 1000000
print(f"{num:,}")  # 1,000,000
```

## 4. 字符串有哪些常用方法？

Python 字符串提供了大量内置方法：

分割与拼接：

```python
# split() 分割字符串
text = "apple,banana,cherry"
fruits = text.split(",")
print(fruits)  # ['apple', 'banana', 'cherry']

# 限制分割次数
text = "a-b-c-d"
print(text.split("-", 2))  # ['a', 'b', 'c-d']

# join() 拼接字符串
words = ["Hello", "World"]
result = " ".join(words)
print(result)  # Hello World

path = "/".join(["usr", "local", "bin"])
print(path)  # usr/local/bin
```

去除空白：

```python
text = "  Hello, World!  "
print(text.strip())   # Hello, World!（去除两端空白）
print(text.lstrip())  # Hello, World!  （去除左端空白）
print(text.rstrip())  #   Hello, World!（去除右端空白）

# 去除指定字符
text = "###hello###"
print(text.strip("#"))  # hello
```

查找与替换：

```python
text = "Hello, World!"

# find() 查找子串位置，找不到返回 -1
print(text.find("World"))  # 7
print(text.find("Python")) # -1

# index() 查找子串位置，找不到抛出 ValueError
# print(text.index("Python"))  # ValueError

# replace() 替换子串
print(text.replace("World", "Python"))  # Hello, Python!

# count() 统计子串出现次数
print("banana".count("a"))  # 3
```

大小写转换与判断：

```python
text = "Hello, World"
print(text.upper())       # HELLO, WORLD
print(text.lower())       # hello, world
print(text.title())       # Hello, World
print(text.capitalize())  # Hello, world
print(text.swapcase())    # hELLO, wORLD

# 判断方法
print("hello".isalpha())    # True（是否全是字母）
print("12345".isdigit())    # True（是否全是数字）
print("hello1".isalnum())   # True（是否全是字母或数字）
print("  ".isspace())       # True（是否全是空白字符）
print("Hello".startswith("He"))  # True
print("Hello".endswith("lo"))    # True
```

## 5. 字符串的切片操作怎么用？

字符串切片使用 [start:stop:step] 语法，可以提取字符串的子串：

```python
text = "Hello, World!"

# 基本切片
print(text[0:5])    # Hello（从索引 0 到 4）
print(text[7:12])   # World
print(text[:5])     # Hello（省略 start，从开头开始）
print(text[7:])     # World!（省略 stop，到末尾结束）
print(text[:])      # Hello, World!（完整复制）

# 负数索引
print(text[-6:])    # orld!
print(text[-6:-1])  # World

# 指定步长
print(text[::2])    # Hlo ol!（每隔一个字符）
print(text[::-1])   # !dlroW ,olleH（反转字符串）

# 实用示例：判断回文串
word = "racecar"
is_palindrome = word == word[::-1]
print(is_palindrome)  # True
```

切片不会导致索引越界错误，即使指定的范围超出字符串长度：

```python
text = "Hello"
print(text[0:100])  # Hello（不会报错）
print(text[100:])   # （空字符串，不会报错）
```

## 6. 字符串的编码与解码是怎么回事？

在 Python 3 中，字符串（str）默认使用 Unicode 编码，可以表示世界上几乎所有的字符。当需要将字符串存储到文件或通过网络传输时，需要将其编码为字节序列（bytes）。

encode() 将字符串编码为字节：

```python
text = "你好，Python"

# 编码为 UTF-8
utf8_bytes = text.encode("utf-8")
print(utf8_bytes)       # b'\xe4\xbd\xa0\xe5\xa5\xbd\xef\xbc\x8cPython'
print(type(utf8_bytes)) # <class 'bytes'>

# 编码为 GBK
gbk_bytes = text.encode("gbk")
print(gbk_bytes)        # b'\xc4\xe3\xba\xc3\xa3\xacPython'
```

decode() 将字节解码为字符串：

```python
# 解码时必须使用相同的编码格式
utf8_bytes = b'\xe4\xbd\xa0\xe5\xa5\xbd'
text = utf8_bytes.decode("utf-8")
print(text)  # 你好

# 使用错误的编码解码会报错或乱码
# utf8_bytes.decode("gbk")  # 可能报错或产生乱码
```

常用编码格式：

- UTF-8：国际通用编码，变长编码，推荐使用
- GBK：中文编码，兼容 GB2312
- ASCII：英文编码，只支持 128 个字符
- Latin-1：西欧语言编码

```python
# 处理编码错误
text = "你好"
bytes_data = text.encode("ascii", errors="ignore")   # 忽略无法编码的字符
print(bytes_data)  # b''

bytes_data = text.encode("ascii", errors="replace")  # 用 ? 替换
print(bytes_data)  # b'??'
```
