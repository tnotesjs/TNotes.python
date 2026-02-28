# [0027. 异常处理](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0027.%20%E5%BC%82%E5%B8%B8%E5%A4%84%E7%90%86)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 什么是异常？常见的内置异常有哪些？](#3--什么是异常常见的内置异常有哪些)
- [4. 🤔 try-except-else-finally 结构怎么用？](#4--try-except-else-finally-结构怎么用)
- [5. 🤔 如何自定义异常？](#5--如何自定义异常)
- [6. 🤔 raise 和异常链是什么？](#6--raise-和异常链是什么)
- [7. 🤔 如何使用断言 assert？](#7--如何使用断言-assert)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- 异常与错误的概念
- try-except 语句
- 捕获多个异常
- else 与 finally 子句
- 自定义异常类
- 断言（assert）的使用

## 2. 🫧 评价

- todo

## 3. 🤔 什么是异常？常见的内置异常有哪些？

异常是程序运行时发生的错误事件，会中断程序的正常执行流程。Python 提供了丰富的内置异常类型：

```python
# 常见内置异常示例

# ValueError：值错误
int("abc")  # ValueError: invalid literal for int()

# TypeError：类型错误
"hello" + 123  # TypeError: can only concatenate str to str

# IndexError：索引超出范围
lst = [1, 2, 3]
lst[10]  # IndexError: list index out of range

# KeyError：字典键不存在
d = {"a": 1}
d["b"]  # KeyError: 'b'

# ZeroDivisionError：除零错误
1 / 0  # ZeroDivisionError: division by zero

# FileNotFoundError：文件不存在
open("nonexistent.txt")  # FileNotFoundError

# AttributeError：属性不存在
"hello".foo()  # AttributeError: 'str' object has no attribute 'foo'

# ImportError：导入失败
import nonexistent_module  # ModuleNotFoundError
```

## 4. 🤔 try-except-else-finally 结构怎么用？

```python
try:
    num = int(input("请输入一个数字："))
    result = 100 / num
except ValueError:
    print("输入的不是有效数字")
except ZeroDivisionError:
    print("不能除以零")
except (TypeError, OverflowError) as e:
    print(f"其它错误：{e}")
else:
    print(f"结果是：{result}")  # 只在无异常时执行
finally:
    print("这里总会执行")  # 无论是否异常都执行
```

各部分的作用：

- try：放置可能抛出异常的代码
- except：捕获并处理特定类型的异常
- else：只在 try 中没有发生异常时执行
- finally：无论是否发生异常都会执行，通常用于资源清理

## 5. 🤔 如何自定义异常？

通过继承 Exception 类创建自定义异常：

```python
class InsufficientBalanceError(Exception):
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        super().__init__(
            f"余额不足：当前余额 {balance} 元，尝试取款 {amount} 元"
        )

class Account:
    def __init__(self, balance):
        self.balance = balance

    def withdraw(self, amount):
        if amount > self.balance:
            raise InsufficientBalanceError(self.balance, amount)
        self.balance -= amount
        return self.balance

account = Account(1000)
try:
    account.withdraw(1500)
except InsufficientBalanceError as e:
    print(e)  # 余额不足：当前余额 1000 元，尝试取款 1500 元
    print(e.balance)  # 1000
    print(e.amount)   # 1500
```

## 6. 🤔 raise 和异常链是什么？

raise 用于主动抛出异常，异常链用于保留原始异常信息：

```python
def validate_age(age):
    if not isinstance(age, int):
        raise TypeError("年龄必须是整数")
    if age < 0 or age > 150:
        raise ValueError(f"无效的年龄：{age}")

try:
    validate_age(-5)
except ValueError as e:
    print(e)  # 无效的年龄：-5
```

异常链（raise ... from ...)：

```python
def parse_config(config_str):
    try:
        return int(config_str)
    except ValueError as e:
        raise RuntimeError("配置解析失败") from e

try:
    parse_config("abc")
except RuntimeError as e:
    print(e)            # 配置解析失败
    print(e.__cause__)  # invalid literal for int() with base 10: 'abc'
```

在 except 中重新抛出异常：

```python
try:
    result = 1 / 0
except ZeroDivisionError:
    print("记录日志...")
    raise  # 重新抛出当前异常
```

## 7. 🤔 如何使用断言 assert？

assert 用于调试和开发阶段的条件检查，如果条件为 False 则抛出 AssertionError：

```python
def calculate_average(numbers):
    assert len(numbers) > 0, "列表不能为空"
    assert all(isinstance(n, (int, float)) for n in numbers), "列表元素必须是数字"
    return sum(numbers) / len(numbers)

print(calculate_average([1, 2, 3]))  # 2.0

try:
    calculate_average([])  # AssertionError: 列表不能为空
except AssertionError as e:
    print(e)
```

注意：assert 不应该用于生产环境的数据验证，因为 Python 用 -O 参数运行时会跳过所有 assert 语句。
