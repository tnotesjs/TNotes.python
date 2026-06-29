# [0053. 打包与分发](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0053.%20%E6%89%93%E5%8C%85%E4%B8%8E%E5%88%86%E5%8F%91)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. pyproject.toml 怎么配置？](#3-pyprojecttoml-怎么配置)
- [4. 如何打包和发布到 PyPI？](#4-如何打包和发布到-pypi)
- [5. 什么是命令行工具？](#5-什么是命令行工具)

<!-- endregion:toc -->

## 1. 本节内容

- setuptools 的使用
- 创建 setup.py
- 发布到 PyPI
- 创建可执行文件（PyInstaller）

## 2. 评价

- todo

## 3. pyproject.toml 怎么配置？

pyproject.toml 是 Python 项目的现代配置文件，替代了 setup.py：

```toml
[build-system]
requires = ["setuptools>=68.0", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "myproject"
version = "1.0.0"
description = "我的 Python 项目"
readme = "README.md"
requires-python = ">=3.10"
license = {text = "MIT"}
authors = [
    {name = "Alice", email = "alice@example.com"}
]

dependencies = [
    "requests>=2.28",
    "click>=8.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.0",
    "black",
    "ruff",
]

[project.scripts]
myapp = "myproject.main:cli"
```

## 4. 如何打包和发布到 PyPI？

```bash
# 安装打包工具
pip install build twine

# 构建分发包
python -m build
# 生成 dist/ 目录：
#   myproject-1.0.0.tar.gz    （源代码包）
#   myproject-1.0.0-py3-none-any.whl  （wheel 包）

# 上传到 TestPyPI（测试）
twine upload --repository testpypi dist/*

# 上传到 PyPI（正式）
twine upload dist/*

# 安装自己的包
pip install myproject
```

## 5. 什么是命令行工具？

使用 click 或 argparse 创建命令行工具：

::: code-group

```python [click]
import click

@click.group()
def cli():
    """我的命令行工具"""
    pass

@cli.command()
@click.argument("name")
@click.option("--greeting", default="你好", help="问候语")
def hello(name, greeting):
    """问候用户"""
    click.echo(f"{greeting}，{name}！")

@cli.command()
@click.option("--count", default=1, help="重复次数")
def repeat(count):
    """重复执行"""
    for i in range(count):
        click.echo(f"第 {i + 1} 次")

if __name__ == "__main__":
    cli()
```

```python [argparse]
import argparse

parser = argparse.ArgumentParser(description="我的工具")
parser.add_argument("name", help="用户名")
parser.add_argument("--greeting", default="你好", help="问候语")
parser.add_argument("-v", "--verbose", action="store_true")

args = parser.parse_args()
print(f"{args.greeting}，{args.name}！")
```

:::
