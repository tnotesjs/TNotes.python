# [0008. 运算符与表达式](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0008.%20%E8%BF%90%E7%AE%97%E7%AC%A6%E4%B8%8E%E8%A1%A8%E8%BE%BE%E5%BC%8F)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. Python 有哪些算术运算符？](#3-python-有哪些算术运算符)
- [4. 比较运算符怎么用？](#4-比较运算符怎么用)
- [5. 赋值运算符有哪些形式？](#5-赋值运算符有哪些形式)
- [6. 逻辑运算符如何使用？](#6-逻辑运算符如何使用)
- [7. 位运算符的作用是什么？](#7-位运算符的作用是什么)
- [8. 成员运算符 in 和 not in 怎么用？](#8-成员运算符-in-和-not-in-怎么用)
- [9. 身份运算符 is 和 is not 有什么作用？](#9-身份运算符-is-和-is-not-有什么作用)
- [10. 运算符的优先级是怎样的？](#10-运算符的优先级是怎样的)

<!-- endregion:toc -->

## 1. 本节内容

- 算术运算符
- 比较运算符
- 赋值运算符
- 逻辑运算符
- 位运算符
- 成员运算符（in、not in）
- 身份运算符（is、is not）
- 运算符优先级

## 2. 评价

- todo

## 3. Python 有哪些算术运算符？

Python 提供了丰富的算术运算符，用于执行数学计算：

```python
a = 10
b = 3

print(a + b)   # 13    加法
print(a - b)   # 7     减法
print(a * b)   # 30    乘法
print(a / b)   # 3.333 除法（结果为浮点数）
print(a // b)  # 3     整除（向下取整）
print(a % b)   # 1     取余
print(a ** b)  # 1000  幂运算（10 的 3 次方）
```

需要注意的地方：

- / 运算符总是返回浮点数，即使两个操作数都是整数
- // 整除运算会向下取整，对于负数需要特别注意
- % 取余运算的结果符号与除数一致

```python
# 整除对负数的处理
print(-7 // 2)   # -4（向下取整，不是向零取整）
print(7 // -2)   # -4

# 取余运算
print(-7 % 2)    # 1
print(7 % -2)    # -1
```

## 4. 比较运算符怎么用？

比较运算符用于比较两个值，返回布尔值 True 或 False：

```python
a = 10
b = 20

print(a == b)   # False  等于
print(a != b)   # True   不等于
print(a > b)    # False  大于
print(a < b)    # True   小于
print(a >= b)   # False  大于等于
print(a <= b)   # True   小于等于
```

Python 支持链式比较，这是一个非常实用的特性：

```python
x = 5
# 链式比较等价于 1 < x and x < 10
print(1 < x < 10)    # True
print(1 < x < 3)     # False

# 也可以用于等值比较
a = b = 5
print(a == b == 5)    # True
```

比较不同类型的值：

```python
# 整数和浮点数可以比较
print(1 == 1.0)       # True
print(1 is 1.0)       # False（类型不同）

# 字符串按字典序比较
print("apple" < "banana")  # True
print("abc" < "abd")       # True
```

## 5. 赋值运算符有哪些形式？

除了基本的赋值运算符 =，Python 还提供了多种复合赋值运算符：

```python
x = 10

x += 5    # 等价于 x = x + 5，结果为 15
x -= 3    # 等价于 x = x - 3，结果为 12
x *= 2    # 等价于 x = x * 2，结果为 24
x /= 4    # 等价于 x = x / 4，结果为 6.0
x //= 2   # 等价于 x = x // 2，结果为 3.0
x %= 2    # 等价于 x = x % 2，结果为 1.0
x **= 3   # 等价于 x = x ** 3，结果为 1.0
```

Python 3.8 引入了海象运算符 :=，可以在表达式中进行赋值：

```python
# 传统写法
line = input()
while line != "quit":
    print(line)
    line = input()

# 使用海象运算符
while (line := input()) != "quit":
    print(line)

# 在列表推导式中使用
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
results = [y for x in numbers if (y := x * 2) > 10]
print(results)  # [12, 14, 16, 18, 20]
```

## 6. 逻辑运算符如何使用？

Python 使用 and、or、not 作为逻辑运算符：

```python
a = True
b = False

print(a and b)  # False  与运算：两者都为 True 才返回 True
print(a or b)   # True   或运算：至少一个为 True 即返回 True
print(not a)    # False  非运算：取反
```

逻辑运算符的短路求值特性：

- and：如果第一个操作数为假，不会计算第二个操作数
- or：如果第一个操作数为真，不会计算第二个操作数

```python
# and 的短路求值
x = 0
# 由于 x 为 0（假值），不会执行 1/x
result = x and 1 / x
print(result)  # 0

# or 的短路求值
name = "" or "默认名称"
print(name)  # 默认名称

# 实际返回值不一定是布尔值，而是决定结果的那个操作数
print(1 and 2)      # 2
print(0 and 2)      # 0
print(1 or 2)       # 1
print(0 or 2)       # 2
print("" or "hello") # hello
```

## 7. 位运算符的作用是什么？

位运算符直接对整数的二进制位进行操作：

```python
a = 0b1100  # 12
b = 0b1010  # 10

print(bin(a & b))   # 0b1000  按位与（都为 1 才为 1）
print(bin(a | b))   # 0b1110  按位或（有一个为 1 就为 1）
print(bin(a ^ b))   # 0b0110  按位异或（不同为 1）
print(bin(~a))      # -0b1101 按位取反
print(bin(a << 2))  # 0b110000 左移 2 位（乘以 4）
print(bin(a >> 1))  # 0b110    右移 1 位（除以 2）
```

位运算的常见应用场景：

```python
# 判断奇偶
n = 7
if n & 1:
    print("奇数")
else:
    print("偶数")

# 交换两个变量（不用临时变量）
a, b = 5, 10
a ^= b
b ^= a
a ^= b
print(a, b)  # 10 5

# 使用位运算实现标志位
READ = 0b001
WRITE = 0b010
EXECUTE = 0b100

permission = READ | WRITE  # 设置读写权限
print(permission & READ)   # 1（有读权限）
print(permission & EXECUTE) # 0（无执行权限）
```

## 8. 成员运算符 in 和 not in 怎么用？

成员运算符用于判断一个值是否存在于序列（字符串、列表、元组、集合、字典）中：

```python
# 在列表中查找
fruits = ["apple", "banana", "cherry"]
print("apple" in fruits)      # True
print("grape" not in fruits)   # True

# 在字符串中查找
text = "Hello, World"
print("Hello" in text)    # True
print("hello" in text)    # False（区分大小写）

# 在元组中查找
colors = ("red", "green", "blue")
print("red" in colors)    # True

# 在集合中查找
numbers = {1, 2, 3, 4, 5}
print(3 in numbers)        # True

# 在字典中查找（默认查找键）
person = {"name": "Alice", "age": 25}
print("name" in person)   # True
print("Alice" in person)  # False（查找的是键，不是值）
print("Alice" in person.values())  # True（查找值）
```

## 9. 身份运算符 is 和 is not 有什么作用？

身份运算符用于判断两个变量是否引用同一个对象（内存地址相同）：

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

# == 比较值是否相等
print(a == b)  # True

# is 比较是否是同一个对象
print(a is b)  # False（虽然值相同，但是两个不同的对象）
print(a is c)  # True（c 和 a 引用同一个对象）

# 可以使用 id() 查看对象的内存地址
print(id(a))   # 例如 140234567890
print(id(b))   # 例如 140234567891（不同地址）
print(id(c))   # 与 a 的地址相同
```

is 和 == 的核心区别：

- is 比较的是对象的身份（内存地址）
- == 比较的是对象的值

与 None 比较时应使用 is：

```python
x = None
# 推荐写法
if x is None:
    print("x 是 None")

# 不推荐写法（虽然通常也能工作）
if x == None:
    print("x 等于 None")
```

Python 对小整数和短字符串有缓存机制（驻留机制），可能出现出乎意料的 is 比较结果：

```python
# 小整数缓存（通常 -5 到 256）
a = 256
b = 256
print(a is b)  # True（缓存范围内）

a = 257
b = 257
print(a is b)  # 可能为 False（超出缓存范围）
```

## 10. 运算符的优先级是怎样的？

Python 运算符按照优先级从高到低排列如下（常用部分）：

| 优先级 | 运算符                       | 说明                 |
| ------ | ---------------------------- | -------------------- |
| 1      | \*\*                         | 幂运算               |
| 2      | ~、+、-（一元运算符）        | 按位取反、正号、负号 |
| 3      | \*、/、//、%                 | 乘、除、整除、取余   |
| 4      | +、-                         | 加、减               |
| 5      | <<、>>                       | 位移                 |
| 6      | &                            | 按位与               |
| 7      | ^                            | 按位异或             |
| 8      | \|                           | 按位或               |
| 9      | ==、!=、>、>=、<、<=、is、in | 比较、身份、成员     |
| 10     | not                          | 逻辑非               |
| 11     | and                          | 逻辑与               |
| 12     | or                           | 逻辑或               |

```python
# 优先级示例
result = 2 + 3 * 4      # 14，先乘后加
result = (2 + 3) * 4    # 20，括号改变优先级
result = 2 ** 3 ** 2     # 512，幂运算从右到左结合
result = not True or False  # False，not 优先于 or
```

当不确定优先级时，建议使用括号明确运算顺序，既能避免错误，也能提高代码可读性。
