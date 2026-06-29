# [0051. 项目结构设计](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0051.%20%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84%E8%AE%BE%E8%AE%A1)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. Python 项目的标准目录结构是什么？](#3-python-项目的标准目录结构是什么)
- [4. 如何管理项目配置？](#4-如何管理项目配置)
- [5. 代码规范与工具有哪些？](#5-代码规范与工具有哪些)

<!-- endregion:toc -->

## 1. 本节内容

- 合理的项目目录组织
- 配置文件管理
- 日志配置
- 错误处理机制

## 2. 评价

- todo

## 3. Python 项目的标准目录结构是什么？

一个规范的 Python 项目通常采用以下结构：

```
myproject/
    src/
        myproject/
            __init__.py
            main.py
            config.py
            models/
                __init__.py
                user.py
            services/
                __init__.py
                auth.py
            utils/
                __init__.py
                helpers.py
    tests/
        __init__.py
        test_main.py
        test_auth.py
    docs/
        index.md
    pyproject.toml
    README.md
    .gitignore
    .env
```

分层原则：

- src/：源代码目录
- tests/：测试代码
- docs/：文档
- pyproject.toml：项目配置（替代 setup.py）

## 4. 如何管理项目配置？

常见的配置管理方式：

::: code-group

```python [环境变量]
import os
from dotenv import load_dotenv  # pip install python-dotenv

load_dotenv()  # 加载 .env 文件

class Config:
    DEBUG = os.getenv("DEBUG", "False").lower() == "true"
    DATABASE_URL = os.getenv("DATABASE_URL", "sqlite:///default.db")
    SECRET_KEY = os.getenv("SECRET_KEY", "dev-secret-key")
    API_KEY = os.getenv("API_KEY")

# .env 文件内容：
# DEBUG=True
# DATABASE_URL=postgresql://user:pass@localhost/mydb
# SECRET_KEY=your-secret-key
```

```python [配置文件]
import tomllib
from pathlib import Path

def load_config(path="config.toml"):
    with open(path, "rb") as f:
        return tomllib.load(f)

config = load_config()
print(config["database"]["host"])

# config.toml 内容：
# [database]
# host = "localhost"
# port = 5432
# name = "mydb"
```

:::

## 5. 代码规范与工具有哪些？

常用的代码规范工具：

```bash
# 代码格式化
pip install black
black src/                # 自动格式化代码

# 导入排序
pip install isort
isort src/                # 自动排序 import 语句

# 代码检查
pip install ruff
ruff check src/           # 快速检查代码问题
ruff check --fix src/     # 自动修复

# 类型检查
pip install mypy
mypy src/                 # 静态类型检查
```

在 pyproject.toml 中配置：

```toml
[tool.black]
line-length = 88

[tool.isort]
profile = "black"

[tool.ruff]
line-length = 88
select = ["E", "F", "I"]

[tool.mypy]
python_version = "3.12"
strict = true
```
