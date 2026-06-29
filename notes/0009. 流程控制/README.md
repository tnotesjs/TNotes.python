# [0009. 流程控制](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0009.%20%E6%B5%81%E7%A8%8B%E6%8E%A7%E5%88%B6)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. if/elif/else 条件语句怎么用？](#3-ifelifelse-条件语句怎么用)
- [4. 什么是条件表达式（三元运算符）？](#4-什么是条件表达式三元运算符)
- [5. while 循环如何使用？](#5-while-循环如何使用)
- [6. for 循环如何使用？](#6-for-循环如何使用)
- [7. range() 函数有哪些用法？](#7-range-函数有哪些用法)
- [8. break、continue、pass 语句分别有什么作用？](#8-breakcontinuepass-语句分别有什么作用)
- [9. 循环的 else 子句是什么？](#9-循环的-else-子句是什么)

<!-- endregion:toc -->

## 1. 本节内容

- 条件语句（if、elif、else）
- 条件表达式（三元运算符）
- while 循环
- for 循环
- range() 函数的使用
- break、continue、pass 语句
- 循环的 else 子句

## 2. 评价

- todo

## 3. if/elif/else 条件语句怎么用？

条件语句根据条件是否成立来决定执行不同的代码块：

```python
age = 18

if age < 18:
    print("未成年")
elif age == 18:
    print("刚好成年")
else:
    print("已成年")
```

if 语句的基本规则：

- if 后面跟条件表达式，以冒号结尾
- 代码块使用缩进表示
- elif 是 else if 的缩写，可以有多个
- else 是可选的，用于处理所有其他情况

```python
# 多个 elif 分支
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print(f"成绩等级：{grade}")  # 成绩等级：B
```

条件可以是任何返回布尔值的表达式，也可以是任何具有真假含义的值：

```python
# 以下值被视为 False
# False, 0, 0.0, "", [], (), {}, None, set()

name = ""
if name:
    print(f"你好，{name}")
else:
    print("名字为空")

# 嵌套的 if 语句
x = 10
if x > 0:
    if x > 100:
        print("大于 100")
    else:
        print("在 0 到 100 之间")
```

## 4. 什么是条件表达式（三元运算符）？

条件表达式是 if-else 语句的简洁写法，适合在一行内完成简单的条件判断：

```python
# 语法：值1 if 条件 else 值2
age = 20
status = "成年" if age >= 18 else "未成年"
print(status)  # 成年

# 等价的 if-else 写法
if age >= 18:
    status = "成年"
else:
    status = "未成年"
```

条件表达式的常见用法：

```python
# 求两个数的较大值
a, b = 10, 20
max_val = a if a > b else b
print(max_val)  # 20

# 在字符串格式化中使用
count = 1
msg = f"有 {count} 个{'项目' if count == 1 else '项目们'}"

# 嵌套条件表达式（不建议过度使用，影响可读性）
x = 0
result = "正数" if x > 0 else ("零" if x == 0 else "负数")
print(result)  # 零
```

## 5. while 循环如何使用？

while 循环在条件为真时重复执行代码块：

```python
# 基本 while 循环
count = 0
while count < 5:
    print(count)
    count += 1
# 输出：0 1 2 3 4

# 用 while 实现累加
total = 0
n = 1
while n <= 100:
    total += n
    n += 1
print(f"1 到 100 的和为：{total}")  # 5050
```

while True 和 break 配合实现需要先执行再判断的场景：

```python
while True:
    user_input = input("请输入一个数字（输入 q 退出）：")
    if user_input == "q":
        break
    print(f"你输入了：{user_input}")
```

注意避免死循环：

```python
# 死循环示例（缺少退出条件）
# while True:
#     print("这是一个死循环")

# 确保循环变量能够改变，最终使条件为 False
```

## 6. for 循环如何使用？

for 循环用于遍历序列（列表、元组、字符串等）或其他可迭代对象：

```python
# 遍历列表
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# 遍历字符串
for char in "Python":
    print(char)

# 遍历字典
person = {"name": "Alice", "age": 25, "city": "Beijing"}
for key in person:
    print(f"{key}: {person[key]}")

# 使用 items() 同时获取键和值
for key, value in person.items():
    print(f"{key}: {value}")

# 使用 enumerate() 获取索引和值
colors = ["red", "green", "blue"]
for index, color in enumerate(colors):
    print(f"{index}: {color}")
```

嵌套循环：

```python
# 打印九九乘法表
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f"{j}×{i}={i*j}", end="\t")
    print()
```

## 7. range() 函数有哪些用法？

range() 函数生成一个整数序列，常与 for 循环配合使用：

```python
# range(stop)：从 0 到 stop-1
for i in range(5):
    print(i)  # 0 1 2 3 4

# range(start, stop)：从 start 到 stop-1
for i in range(2, 6):
    print(i)  # 2 3 4 5

# range(start, stop, step)：指定步长
for i in range(0, 10, 2):
    print(i)  # 0 2 4 6 8

# 负数步长（倒序）
for i in range(10, 0, -1):
    print(i)  # 10 9 8 7 6 5 4 3 2 1

# range 返回的是一个 range 对象，不是列表
r = range(5)
print(type(r))    # <class 'range'>
print(list(r))    # [0, 1, 2, 3, 4]
```

range 对象是惰性的，不会一次性生成所有数字，因此即使范围很大也不会占用大量内存：

```python
# 不会占用大量内存
r = range(1_000_000)
print(len(r))        # 1000000
print(999_999 in r)  # True
```

## 8. break、continue、pass 语句分别有什么作用？

break 语句用于立即退出循环：

```python
# 找到第一个偶数就停止
numbers = [1, 3, 5, 8, 9, 11]
for n in numbers:
    if n % 2 == 0:
        print(f"找到偶数：{n}")
        break
# 输出：找到偶数：8
```

continue 语句用于跳过当前循环的剩余部分，进入下一次循环：

```python
# 打印所有奇数
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)
# 输出：1 3 5 7 9
```

pass 语句是一个空操作，什么也不做，用作占位符：

```python
# 定义一个空函数（稍后实现）
def todo_function():
    pass

# 定义一个空类
class MyClass:
    pass

# 在条件语句中占位
if True:
    pass  # 暂时不做任何处理
else:
    print("else 分支")
```

## 9. 循环的 else 子句是什么？

Python 的 for 和 while 循环可以带有 else 子句。else 中的代码在循环正常结束时执行，但如果循环被 break 中断，则不会执行 else。

```python
# 循环正常结束，else 会执行
for i in range(5):
    print(i)
else:
    print("循环正常结束")
# 输出：0 1 2 3 4 循环正常结束

# 循环被 break 中断，else 不会执行
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("这行不会被执行")
# 输出：0 1 2
```

一个实用的例子是在查找场景中使用 for-else：

```python
# 检查列表中是否存在目标值
numbers = [1, 3, 5, 7, 9]
target = 4

for n in numbers:
    if n == target:
        print(f"找到了 {target}")
        break
else:
    print(f"没有找到 {target}")
# 输出：没有找到 4
```

while 循环也可以使用 else 子句：

```python
count = 0
while count < 3:
    print(count)
    count += 1
else:
    print("while 循环正常结束")
# 输出：0 1 2 while 循环正常结束
```
