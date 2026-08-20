# [0004. 初识 Python](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0004.%20%E5%88%9D%E8%AF%86%20Python)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. Python 的历史与发展历程是怎样的？](#2-python-的历史与发展历程是怎样的)
- [3. Python 有哪些特点和应用领域？](#3-python-有哪些特点和应用领域)
- [4. Python 2 和 Python 3 有什么区别？](#4-python-2-和-python-3-有什么区别)
- [5. 如何安装 Python 解释器？](#5-如何安装-python-解释器)
- [6. 如何编写并运行第一个 Python 程序？](#6-如何编写并运行第一个-python-程序)
- [7. 运行 Python 代码有哪些方式？](#7-运行-python-代码有哪些方式)

<!-- endregion:toc -->

## 1. 本节内容

- Python 的历史与发展
- Python 的特点与应用领域
- Python 2 vs Python 3
- 安装 Python 解释器
- 第一个 Python 程序（Hello World）
- 运行 Python 代码的多种方式（交互式、脚本、IDE）

## 2. Python 的历史与发展历程是怎样的？

Python 由荷兰程序员 Guido van Rossum 于 1989 年圣诞节期间开始设计，1991 年发布了第一个公开版本 0.9.0。Guido 最初是为了打发圣诞节假期的无聊时光，同时也希望创造一门既易于阅读又功能强大的编程语言。

Python 这个名字来源于 Guido 喜欢的一档英国喜剧节目「Monty Python's Flying Circus」，而非蟒蛇。

主要发展里程碑：

- 1991 年，Python 0.9.0 发布，已包含类、函数、异常处理、列表和字典等核心数据类型
- 1994 年，Python 1.0 发布，引入了 lambda、map、filter、reduce 等函数式编程特性
- 2000 年，Python 2.0 发布，引入了列表推导式、垃圾回收机制
- 2008 年，Python 3.0 发布，对语言做了重大改进，不向后兼容 Python 2
- 2020 年，Python 2 正式停止维护
- 至今，Python 3 持续演进，已成为全球最受欢迎的编程语言之一

## 3. Python 有哪些特点和应用领域？

Python 的核心特点：

- 语法简洁，可读性强，接近自然语言
- 动态类型，变量无需声明类型
- 解释型语言，无需编译即可运行
- 跨平台，可在 Windows、macOS、Linux 等系统上运行
- 拥有丰富的标准库和第三方库
- 支持多种编程范式（面向对象、函数式、过程式）
- 社区庞大，生态活跃

主要应用领域：

- Web 开发：Django、Flask、FastAPI 等框架
- 数据科学与分析：NumPy、Pandas、Matplotlib 等库
- 人工智能与机器学习：TensorFlow、PyTorch、scikit-learn 等框架
- 自动化脚本：系统管理、文件处理、定时任务
- 爬虫开发：Scrapy、BeautifulSoup、requests 等工具
- 科学计算：SciPy、SymPy 等库
- 游戏开发：Pygame 等库
- 桌面应用：Tkinter、PyQt 等 GUI 框架

## 4. Python 2 和 Python 3 有什么区别？

Python 3 于 2008 年发布，对 Python 2 做了许多不向后兼容的改进。Python 2 已于 2020 年 1 月 1 日正式停止维护，新项目应当使用 Python 3。

主要区别：

| 特性     | Python 2               | Python 3               |
| -------- | ---------------------- | ---------------------- |
| print    | print "hello"（语句）  | print("hello")（函数） |
| 整数除法 | 3 / 2 得到 1           | 3 / 2 得到 1.5         |
| 字符串   | 默认 ASCII             | 默认 Unicode           |
| input    | raw_input() 获取字符串 | input() 获取字符串     |
| range    | range() 返回列表       | range() 返回迭代器     |
| 异常语法 | except Exception, e    | except Exception as e  |

::: code-group

```python [Python 2]
# Python 2 中的 print 是语句
print "Hello, World!"

# 整数除法结果为整数
result = 3 / 2  # 结果为 1

# 获取用户输入
name = raw_input("请输入你的名字：")
```

```python [Python 3]
# Python 3 中的 print 是函数
print("Hello, World!")

# 整数除法结果为浮点数
result = 3 / 2  # 结果为 1.5

# 获取用户输入
name = input("请输入你的名字：")
```

:::

## 5. 如何安装 Python 解释器？

不同操作系统的安装方式不同：

在 Windows 上安装：

1. 访问 Python 官网 https://www.python.org/downloads/
2. 下载最新版本的 Windows 安装包
3. 运行安装程序，注意勾选 Add Python to PATH 选项
4. 点击 Install Now 完成安装

在 macOS 上安装：

macOS 通常自带 Python，但版本可能较旧。推荐使用 Homebrew 安装：

```bash
brew install python3
```

在 Linux 上安装：

大多数 Linux 发行版自带 Python 3。如果需要安装或更新：

::: code-group

```bash [Ubuntu/Debian]
sudo apt update
sudo apt install python3
```

```bash [CentOS/RHEL]
sudo yum install python3
```

:::

验证安装是否成功：

```bash
python3 --version
```

## 6. 如何编写并运行第一个 Python 程序？

最经典的第一个程序就是输出 Hello World。

创建一个名为 hello.py 的文件，写入以下代码：

```python
print("Hello, World!")
```

在终端中运行：

```bash
python3 hello.py
```

输出结果：

```
Hello, World!
```

也可以编写一些稍微复杂的程序，比如和用户交互：

```python
name = input("请输入你的名字：")
print(f"你好，{name}！欢迎学习 Python。")
```

## 7. 运行 Python 代码有哪些方式？

运行 Python 代码主要有以下几种方式：

交互式解释器（REPL）：

在终端输入 python3 即可进入交互模式，适合快速测试代码片段。

```bash
$ python3
>>> 2 + 3
5
>>> print("Hello")
Hello
>>> exit()
```

脚本文件方式：

将代码保存为 .py 文件，通过命令行运行。这是最常用的方式。

```bash
python3 script.py
```

IDE 运行：

使用集成开发环境（如 PyCharm、VS Code）编写代码，直接点击运行按钮或使用快捷键执行。IDE 提供了代码补全、调试、语法高亮等功能，可以显著提升开发效率。

Jupyter Notebook：

以单元格（cell）为单位编写和运行代码，适合数据分析、机器学习等场景。可以将代码、文本、图表混合在一个文档中。

```bash
# 安装 Jupyter
pip install jupyter

# 启动 Jupyter Notebook
jupyter notebook
```

使用 -c 参数直接执行代码：

```bash
python3 -c "print('Hello from command line')"
```

使用 -m 参数运行模块：

```bash
python3 -m http.server 8000
```
