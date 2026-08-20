# [0023. 继承与多态](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0023.%20%E7%BB%A7%E6%89%BF%E4%B8%8E%E5%A4%9A%E6%80%81)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 什么是单继承与方法重写？](#2-什么是单继承与方法重写)
- [3. super() 函数怎么用？](#3-super-函数怎么用)
- [4. 什么是多重继承与 MRO？](#4-什么是多重继承与-mro)
- [5. 什么是多态与鸭子类型？](#5-什么是多态与鸭子类型)

<!-- endregion:toc -->

## 1. 本节内容

- 单继承与父类方法重写
- super() 函数的使用
- 多重继承与 MRO（方法解析顺序）
- 多态与鸭子类型

## 2. 什么是单继承与方法重写？

继承允许一个类（子类）继承另一个类（父类）的属性和方法。子类可以重写父类的方法来提供不同的实现。

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} 发出声音"

    def info(self):
        return f"动物：{self.name}"

class Dog(Animal):  # Dog 继承自 Animal
    def speak(self):  # 重写父类方法
        return f"{self.name} 汪汪叫"

class Cat(Animal):
    def speak(self):
        return f"{self.name} 喵喵叫"

dog = Dog("大黄")
cat = Cat("小花")

print(dog.speak())  # 大黄 汪汪叫
print(cat.speak())  # 小花 喵喵叫
print(dog.info())   # 动物：大黄（继承自父类）

# 检查继承关系
print(isinstance(dog, Dog))     # True
print(isinstance(dog, Animal))  # True
print(issubclass(Dog, Animal))  # True
```

## 3. super() 函数怎么用？

super() 用于调用父类的方法，常用于在子类中扩展父类的功能：

```python
class Animal:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Dog(Animal):
    def __init__(self, name, age, breed):
        super().__init__(name, age)  # 调用父类的 __init__
        self.breed = breed           # 添加子类特有的属性

    def info(self):
        return f"{self.name}，{self.age} 岁，品种：{self.breed}"

dog = Dog("大黄", 3, "金毛")
print(dog.info())  # 大黄，3 岁，品种：金毛
```

在重写方法中使用 super() 扩展功能：

```python
class Logger:
    def log(self, message):
        print(f"[LOG] {message}")

class TimestampLogger(Logger):
    def log(self, message):
        from datetime import datetime
        timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        super().log(f"{timestamp} - {message}")

logger = TimestampLogger()
logger.log("系统启动")
# [LOG] 2026-02-28 10:30:00 - 系统启动
```

## 4. 什么是多重继承与 MRO？

Python 支持多重继承，即一个类可以继承多个父类：

```python
class Flyable:
    def fly(self):
        return "我会飞"

class Swimmable:
    def swim(self):
        return "我会游泳"

class Duck(Flyable, Swimmable):
    def quack(self):
        return "嘎嘎嘎"

duck = Duck()
print(duck.fly())    # 我会飞
print(duck.swim())   # 我会游泳
print(duck.quack())  # 嘎嘎嘎
```

MRO（Method Resolution Order，方法解析顺序）决定了多重继承时方法的查找顺序：

```python
class A:
    def greet(self):
        return "A"

class B(A):
    def greet(self):
        return "B"

class C(A):
    def greet(self):
        return "C"

class D(B, C):
    pass

d = D()
print(d.greet())  # B

# 查看 MRO
print(D.__mro__)
# (<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>)
# Python 使用 C3 线性化算法确定 MRO
```

## 5. 什么是多态与鸭子类型？

多态是指不同类型的对象可以响应相同的消息（方法调用）：

```python
class Dog:
    def speak(self):
        return "汪汪"

class Cat:
    def speak(self):
        return "喵喵"

class Duck:
    def speak(self):
        return "嘎嘎"

# 多态：同一个函数可以处理不同类型的对象
def animal_speak(animal):
    print(animal.speak())

animal_speak(Dog())   # 汪汪
animal_speak(Cat())   # 喵喵
animal_speak(Duck())  # 嘎嘎
```

Python 采用鸭子类型（Duck Typing）的理念：“如果它走起来像鸭子，叫起来像鸭子，那它就是鸭子”。不关心对象的类型，只关心对象是否有对应的方法。

```python
class Robot:
    def speak(self):
        return "滴滴答答"

# Robot 不是动物，但只要有 speak 方法就可以使用
animal_speak(Robot())  # 滴滴答答
```

Python 也支持通过抽象基类实现更严格的接口约束：

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

# shape = Shape()  # TypeError：不能实例化抽象类
rect = Rectangle(5, 3)
print(rect.area())       # 15
print(rect.perimeter())  # 16
```
