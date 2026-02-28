# [0024. 封装与访问控制](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0024.%20%E5%B0%81%E8%A3%85%E4%B8%8E%E8%AE%BF%E9%97%AE%E6%8E%A7%E5%88%B6)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 Python 中的公开属性与私有属性是什么？](#3--python-中的公开属性与私有属性是什么)
- [4. 🤔 property 装饰器怎么用？](#4--property-装饰器怎么用)
- [5. 🤔 什么是静态方法 @staticmethod？](#5--什么是静态方法-staticmethod)
- [6. 🤔 什么是类方法 @classmethod？](#6--什么是类方法-classmethod)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- 公开属性与私有属性（命名修饰）
- property 装饰器（getter、setter、deleter）
- 静态方法（@staticmethod）
- 类方法（@classmethod）

## 2. 🫧 评价

- todo

## 3. 🤔 Python 中的公开属性与私有属性是什么？

Python 通过命名约定来实现访问控制，而不是像 Java 那样使用关键字：

```python
class Person:
    def __init__(self, name, age, salary):
        self.name = name       # 公开属性：可以自由访问
        self._age = age        # 受保护属性：约定不应在类外部访问
        self.__salary = salary # 私有属性：名称修饰，难以直接访问

p = Person("Alice", 25, 50000)

# 公开属性
print(p.name)     # Alice

# 受保护属性（可以访问，但约定不应该）
print(p._age)     # 25

# 私有属性（名称被修改了）
# print(p.__salary)  # AttributeError
print(p._Person__salary)  # 50000（可以通过名称修饰访问，但不推荐）
```

命名规则总结：

- name：公开属性
- \_name：受保护属性（约定，非强制）
- **name：私有属性（名称修饰，变为 \_ClassName**name）
- `__name__`：特殊属性（魔法属性，由 Python 定义）

## 4. 🤔 property 装饰器怎么用？

property 装饰器可以将方法伪装成属性，提供更优雅的访问控制：

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius

    @property
    def celsius(self):
        """getter：获取摄氏度"""
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        """setter：设置摄氏度，带验证"""
        if value < -273.15:
            raise ValueError("温度不能低于绝对零度")
        self._celsius = value

    @celsius.deleter
    def celsius(self):
        """deleter：删除属性"""
        print("删除温度属性")
        del self._celsius

    @property
    def fahrenheit(self):
        """只读属性：华氏度"""
        return self._celsius * 9 / 5 + 32

t = Temperature(100)
print(t.celsius)      # 100（像访问属性一样）
print(t.fahrenheit)   # 212.0

t.celsius = 0         # 像赋值属性一样，实际调用了 setter
print(t.fahrenheit)   # 32.0

# t.celsius = -300    # ValueError：温度不能低于绝对零度
# t.fahrenheit = 100  # AttributeError：只读属性不能赋值
```

## 5. 🤔 什么是静态方法 @staticmethod？

静态方法不需要访问实例或类，类似于普通函数，只是逻辑上属于某个类：

```python
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b

    @staticmethod
    def is_even(n):
        return n % 2 == 0

# 通过类名调用
print(MathUtils.add(3, 5))      # 8
print(MathUtils.is_even(4))     # True

# 也可以通过实例调用
m = MathUtils()
print(m.add(3, 5))  # 8
```

## 6. 🤔 什么是类方法 @classmethod？

类方法的第一个参数是类本身（通常命名为 cls），而不是实例：

```python
class Date:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day

    @classmethod
    def from_string(cls, date_string):
        """从字符串创建 Date 实例（工厂方法）"""
        year, month, day = map(int, date_string.split("-"))
        return cls(year, month, day)

    @classmethod
    def today(cls):
        """创建今天的 Date 实例"""
        from datetime import date
        d = date.today()
        return cls(d.year, d.month, d.day)

    def __repr__(self):
        return f"Date({self.year}, {self.month}, {self.day})"

# 使用类方法创建实例
d1 = Date.from_string("2026-02-28")
d2 = Date.today()
print(d1)  # Date(2026, 2, 28)
print(d2)  # Date(今天的日期)
```

静态方法与类方法的区别：

- 静态方法：不接收 self 或 cls，与类和实例无关
- 类方法：接收 cls，可以访问类属性，常用作工厂方法
