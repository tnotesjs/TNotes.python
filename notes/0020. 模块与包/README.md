# [0020. 模块与包](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0020.%20%E6%A8%A1%E5%9D%97%E4%B8%8E%E5%8C%85)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 模块的导入方式有哪些？](#3--模块的导入方式有哪些)
- [4. 🤔 模块搜索路径是怎样的？](#4--模块搜索路径是怎样的)
- [5. 🤔 if **name** == '**main**' 有什么作用？](#5--if-name--main-有什么作用)
- [6. 🤔 如何创建和组织包？](#6--如何创建和组织包)
- [7. 🤔 相对导入和绝对导入有什么区别？](#7--相对导入和绝对导入有什么区别)
- [8. 🤔 有哪些常用的内置模块？](#8--有哪些常用的内置模块)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- 模块的导入（import、from...import）
- 模块搜索路径
- `if __name__ == '__main__'` 的作用
- 包的创建与组织
- 相对导入与绝对导入
- 常用内置模块介绍（sys、os、math、random、datetime 等）

## 2. 🫧 评价

- todo

## 3. 🤔 模块的导入方式有哪些？

模块是一个包含 Python 代码的 .py 文件。导入模块有多种方式：

```python
# 导入整个模块
import math
print(math.sqrt(16))  # 4.0

# 导入模块并起别名
import numpy as np

# 从模块中导入特定对象
from math import sqrt, pi
print(sqrt(16))  # 4.0
print(pi)        # 3.141592653589793

# 导入并起别名
from math import factorial as fact
print(fact(5))  # 120

# 导入模块中的所有公开对象（不推荐，可能导致命名冲突）
from math import *
```

## 4. 🤔 模块搜索路径是怎样的？

当导入模块时，Python 会按照以下顺序搜索模块：

1. 当前目录
2. PYTHONPATH 环境变量指定的目录
3. Python 安装目录的标准库路径
4. 第三方包的安装目录（site-packages）

```python
import sys

# 查看模块搜索路径
for path in sys.path:
    print(path)

# 动态添加搜索路径
sys.path.append("/path/to/my/modules")
```

## 5. 🤔 if **name** == '**main**' 有什么作用？

每个 Python 模块都有一个 `__name__` 属性。当模块被直接运行时，`__name__` 的值为 `'__main__'`；当模块被导入时，`__name__` 的值为模块名。

```python
# mymodule.py
def greet(name):
    print(f"你好，{name}")

def main():
    greet("World")

if __name__ == "__main__":
    # 只有直接运行此文件时才执行
    main()
```

这样设计的好处是：

- 直接运行 python mymodule.py 时会执行 main() 函数
- 其他文件通过 import mymodule 导入时不会执行 main()，只能调用其中的函数

## 6. 🤔 如何创建和组织包？

包（package）是一个包含 `__init__.py` 文件的目录，用于组织多个相关模块。

目录结构示例：

```
my_package/
    __init__.py
    module_a.py
    module_b.py
    sub_package/
        __init__.py
        module_c.py
```

`__init__.py` 可以为空，也可以用来定义包的公开接口：

```python
# my_package/__init__.py
from .module_a import func_a
from .module_b import func_b

__all__ = ["func_a", "func_b"]
```

使用包：

```python
# 导入包中的模块
import my_package.module_a
my_package.module_a.func_a()

# 从包中导入
from my_package import module_a
module_a.func_a()

# 从包中直接导入函数
from my_package.module_a import func_a
func_a()

# 导入子包
from my_package.sub_package import module_c
```

## 7. 🤔 相对导入和绝对导入有什么区别？

绝对导入使用完整的包路径，相对导入使用的界引用当前包的位置。

::: code-group

```python [绝对导入]
# 使用完整路径
from my_package.module_a import func_a
from my_package.sub_package.module_c import func_c
```

```python [相对导入]
# 在 my_package/module_b.py 中
from .module_a import func_a           # 当前包
from ..other_package import module_d   # 父包
from .sub_package import module_c      # 子包
```

:::

相对导入的规则：

- `.` 表示当前包
- `..` 表示父包
- `...` 表示父包的父包
- 相对导入只能在包内使用，不能在须直接运行的脚本中使用

## 8. 🤔 有哪些常用的内置模块？

Python 标准库提供了大量实用的内置模块：

```python
import os
# 文件和目录操作
print(os.getcwd())               # 获取当前工作目录
print(os.listdir("."))           # 列出当前目录文件
print(os.path.exists("test.py")) # 判断文件是否存在
```

```python
import sys
# 系统相关
print(sys.version)     # Python 版本
print(sys.platform)    # 操作系统平台
print(sys.argv)        # 命令行参数
```

```python
import math
print(math.pi)          # 3.141592653589793
print(math.sqrt(2))     # 1.4142135623730951
print(math.ceil(3.2))   # 4
print(math.floor(3.8))  # 3
```

```python
import random
print(random.randint(1, 100))       # 1 到 100 的随机整数
print(random.choice(["a", "b", "c"])) # 随机选择一个元素
print(random.random())               # 0 到 1 的随机浮点数
```

```python
from datetime import datetime, timedelta
now = datetime.now()
print(now)                                # 当前时间
print(now.strftime("%Y-%m-%d %H:%M:%S"))  # 格式化时间
tomorrow = now + timedelta(days=1)        # 时间计算
```
