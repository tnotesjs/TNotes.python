# [0022. 类与对象基础](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0022.%20%E7%B1%BB%E4%B8%8E%E5%AF%B9%E8%B1%A1%E5%9F%BA%E7%A1%80)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 什么是面向对象编程思想？](#2-什么是面向对象编程思想)
- [3. 如何定义类和创建实例？](#3-如何定义类和创建实例)
- [4. 实例属性和类属性有什么区别？](#4-实例属性和类属性有什么区别)
- [5. 实例方法与 self 参数是什么？](#5-实例方法与-self-参数是什么)
- [6. 构造方法 **init** 怎么用？](#6-构造方法-init-怎么用)
- [7. 析构方法 **del** 是什么？](#7-析构方法-del-是什么)

<!-- endregion:toc -->

## 1. 本节内容

- 面向对象编程思想
- 类的定义与实例化
- 实例属性与类属性
- 实例方法与 self 参数
- 构造方法 `__init__`
- 析构方法 `__del__`

## 2. 什么是面向对象编程思想？

面向对象编程（Object-Oriented Programming，OOP）是一种以对象为核心的编程范式。它将数据和操作数据的方法封装在一起，形成对象。

OOP 的三大特征：

- 封装：将数据和方法包装在类中，隐藏内部实现细节
- 继承：子类可以继承父类的属性和方法，实现代码复用
- 多态：不同对象对同一消息可以有不同的响应

类是对象的蓝图（模板），对象是类的实例：

```python
# 类好比设计图纸
class Dog:
    pass

# 对象是按照图纸制造出来的实体
dog1 = Dog()
dog2 = Dog()

# 每个对象是独立的
print(dog1 is dog2)  # False
```

## 3. 如何定义类和创建实例？

使用 class 关键字定义类，通过调用类名创建实例：

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        print(f"我叫 {self.name}，今年 {self.age} 岁")

# 创建实例
s1 = Student("Alice", 20)
s2 = Student("Bob", 22)

s1.introduce()  # 我叫 Alice，今年 20 岁
s2.introduce()  # 我叫 Bob，今年 22 岁

# 访问属性
print(s1.name)  # Alice
print(s2.age)   # 22

# 修改属性
s1.age = 21
print(s1.age)   # 21
```

## 4. 实例属性和类属性有什么区别？

实例属性属于每个对象，各自独立；类属性属于类本身，所有实例共享。

```python
class Dog:
    # 类属性：所有实例共享
    species = "Canis familiaris"
    count = 0

    def __init__(self, name):
        # 实例属性：每个实例独立
        self.name = name
        Dog.count += 1

d1 = Dog("Buddy")
d2 = Dog("Max")

# 类属性通过类名或实例访问
print(Dog.species)   # Canis familiaris
print(d1.species)    # Canis familiaris
print(Dog.count)     # 2

# 实例属性只属于各自的对象
print(d1.name)  # Buddy
print(d2.name)  # Max
```

注意：通过实例修改类属性时，实际上是创建了一个同名的实例属性，不会影响类属性：

```python
d1.species = "Modified"
print(d1.species)    # Modified（实例属性）
print(d2.species)    # Canis familiaris（类属性未变）
print(Dog.species)   # Canis familiaris（类属性未变）
```

## 5. 实例方法与 self 参数是什么？

实例方法是定义在类中的函数，第一个参数必须是 self，代表实例本身：

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        import math
        return math.pi * self.radius ** 2

    def perimeter(self):
        import math
        return 2 * math.pi * self.radius

    def resize(self, new_radius):
        self.radius = new_radius

c = Circle(5)
print(c.area())        # 78.53981633974483
print(c.perimeter())   # 31.41592653589793

c.resize(10)
print(c.area())        # 314.1592653589793
```

self 不是关键字，只是约定俗成的参数名。调用方法时不需要手动传入 self，Python 会自动传入。

## 6. 构造方法 **init** 怎么用？

`__init__` 是类的构造方法，在创建实例时自动调用，用于初始化实例属性：

```python
class Person:
    def __init__(self, name, age, email=None):
        self.name = name
        self.age = age
        self.email = email or "unknown"

    def info(self):
        return f"{self.name}, {self.age} 岁, {self.email}"

# 创建实例时自动调用 __init__
p1 = Person("Alice", 25, "alice@example.com")
p2 = Person("Bob", 30)

print(p1.info())  # Alice, 25 岁, alice@example.com
print(p2.info())  # Bob, 30 岁, unknown
```

`__init__` 的特点：

- 不能有返回值（不能使用 return 返回非 None 的值）
- 一个类只能有一个 `__init__` 方法，但可以通过默认参数实现类似多个构造函数的效果

## 7. 析构方法 **del** 是什么？

`__del__` 是析构方法，在对象被垃圾回收时自动调用，用于释放资源：

```python
class FileHandler:
    def __init__(self, filename):
        self.filename = filename
        self.file = open(filename, "w")
        print(f"打开文件：{filename}")

    def write(self, content):
        self.file.write(content)

    def __del__(self):
        self.file.close()
        print(f"关闭文件：{self.filename}")

# 创建对象
fh = FileHandler("test.txt")
fh.write("Hello")

# 删除对象时触发 __del__
del fh  # 关闭文件：test.txt
```

在实践中，不建议依赖 `__del__` 来管理资源，因为它的调用时机不确定。推荐使用上下文管理器（with 语句）或显式的 close() 方法。
