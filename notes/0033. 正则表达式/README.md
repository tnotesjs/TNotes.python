# [0033. 正则表达式](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0033.%20%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 正则表达式的基本语法是什么？](#2-正则表达式的基本语法是什么)
- [3. re 模块有哪些常用函数？](#3-re-模块有哪些常用函数)
- [4. 分组与引用怎么用？](#4-分组与引用怎么用)
- [5. 正则表达式有哪些实用场景？](#5-正则表达式有哪些实用场景)

<!-- endregion:toc -->

## 1. 本节内容

- 正则表达式语法
- re 模块的使用（match、search、findall、sub）
- 编译正则表达式
- 分组与捕获

## 2. 正则表达式的基本语法是什么？

正则表达式是用于匹配字符串模式的语言，Python 通过 re 模块提供支持：

```python
import re

# 常用元字符
# .   匹配任意字符（除换行）
# \d  匹配数字 [0-9]
# \w  匹配字母、数字、下划线
# \s  匹配空白字符
# ^   匹配开头
# $   匹配结尾
# *   重复 0 次或更多
# +   重复 1 次或更多
# ?   重复 0 次或 1 次
# {n} 重复 n 次
# {n,m} 重复 n 到 m 次
# []  字符集
# |   或
# () 分组

# 示例
print(re.match(r"\d+", "123abc"))       # 匹配开头的数字
print(re.search(r"\d+", "abc123def"))   # 搜索第一个匹配
print(re.findall(r"\d+", "a1b2c3"))    # 找所有匹配：['1', '2', '3']
```

## 3. re 模块有哪些常用函数？

```python
import re

text = "我的邮箱是 alice@example.com，备用是 bob@test.org"

# search：找第一个匹配
match = re.search(r"\w+@\w+\.\w+", text)
if match:
    print(match.group())  # alice@example.com

# findall：找所有匹配
emails = re.findall(r"\w+@\w+\.\w+", text)
print(emails)  # ['alice@example.com', 'bob@test.org']

# sub：替换
result = re.sub(r"\d+", "*", "电话 13812345678")
print(result)  # 电话 *

# split：分割
parts = re.split(r"[,;、]", "苹果,香蕉;橘子、葡萄")
print(parts)  # ['苹果', '香蕉', '橘子', '葡萄']

# compile：预编译正则（多次使用时更高效）
pattern = re.compile(r"\d{4}-\d{2}-\d{2}")
dates = pattern.findall("日期：2026-01-15 和 2026-02-28")
print(dates)  # ['2026-01-15', '2026-02-28']
```

## 4. 分组与引用怎么用？

分组用于提取匹配中的特定部分：

```python
import re

# 基本分组
match = re.search(r"(\d{4})-(\d{2})-(\d{2})", "today is 2026-02-28")
if match:
    print(match.group())   # 2026-02-28（完整匹配）
    print(match.group(1))  # 2026（第一个分组）
    print(match.group(2))  # 02
    print(match.group(3))  # 28
    print(match.groups())  # ('2026', '02', '28')

# 命名分组
match = re.search(
    r"(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})",
    "2026-02-28"
)
if match:
    print(match.group("year"))   # 2026
    print(match.group("month"))  # 02
    print(match.groupdict())     # {'year': '2026', 'month': '02', 'day': '28'}

# findall 与分组
results = re.findall(r"(\w+)@(\w+\.\w+)", "alice@a.com bob@b.org")
print(results)  # [('alice', 'a.com'), ('bob', 'b.org')]
```

## 5. 正则表达式有哪些实用场景？

```python
import re

# 验证邮箱
def is_valid_email(email):
    pattern = r"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"
    return bool(re.match(pattern, email))

print(is_valid_email("alice@example.com"))  # True
print(is_valid_email("invalid@"))           # False

# 验证手机号
def is_valid_phone(phone):
    pattern = r"^1[3-9]\d{9}$"
    return bool(re.match(pattern, phone))

print(is_valid_phone("13812345678"))  # True

# 提取 HTML 标签内容
html = "<h1>标题</h1><p>正文</p>"
tags = re.findall(r"<(\w+)>(.*?)</\1>", html)
print(tags)  # [('h1', '标题'), ('p', '正文')]

# 清理字符串
text = "  多个   空格   的   文本  "
cleaned = re.sub(r"\s+", " ", text.strip())
print(cleaned)  # 多个 空格 的 文本
```
