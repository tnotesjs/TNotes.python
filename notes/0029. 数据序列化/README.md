# [0029. 数据序列化](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0029.%20%E6%95%B0%E6%8D%AE%E5%BA%8F%E5%88%97%E5%8C%96)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. 什么是 JSON 序列化？](#3-什么是-json-序列化)
- [4. 什么是 CSV 文件处理？](#4-什么是-csv-文件处理)
- [5. 什么是 pickle 序列化？](#5-什么是-pickle-序列化)
- [6. 如何使用 YAML 和 TOML？](#6-如何使用-yaml-和-toml)

<!-- endregion:toc -->

## 1. 本节内容

- JSON 数据的读写
- CSV 文件的处理（csv 模块）
- 使用 pickle 进行对象序列化
- XML 与 YAML 简介

## 2. 评价

- todo

## 3. 什么是 JSON 序列化？

JSON（JavaScript Object Notation）是最常用的数据交换格式，Python 通过 json 模块来处理：

::: code-group

```python [基本操作]
import json

# Python 对象转 JSON 字符串
data = {
    "name": "Alice",
    "age": 25,
    "hobbies": ["读书", "编程"],
    "address": {"city": "北京", "zip": "100000"}
}

json_str = json.dumps(data, ensure_ascii=False, indent=2)
print(json_str)

# JSON 字符串转 Python 对象
parsed = json.loads(json_str)
print(parsed["name"])  # Alice
```

```python [文件操作]
import json

data = {"users": [{"name": "Alice"}, {"name": "Bob"}]}

# 写入 JSON 文件
with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)

# 读取 JSON 文件
with open("data.json", "r", encoding="utf-8") as f:
    loaded = json.load(f)
    print(loaded)
```

:::

## 4. 什么是 CSV 文件处理？

CSV（Comma-Separated Values）是常用的表格数据格式：

::: code-group

```python [写入 CSV]
import csv

# 写入
headers = ["姓名", "年龄", "城市"]
rows = [
    ["张三", 25, "北京"],
    ["李四", 30, "上海"],
    ["王五", 28, "广州"],
]

with open("data.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.writer(f)
    writer.writerow(headers)
    writer.writerows(rows)
```

```python [读取 CSV]
import csv

# 读取
with open("data.csv", "r", encoding="utf-8") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# 使用 DictReader
with open("data.csv", "r", encoding="utf-8") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["姓名"], row["年龄"])
```

:::

## 5. 什么是 pickle 序列化？

pickle 用于将 Python 对象序列化为二进制格式，支持几乎所有 Python 类型：

```python
import pickle

# 复杂对象
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

user = User("Alice", 25)
data = {
    "users": [user],
    "count": 1,
    "tags": {"admin", "active"}
}

# 序列化到文件
with open("data.pkl", "wb") as f:
    pickle.dump(data, f)

# 从文件反序列化
with open("data.pkl", "rb") as f:
    loaded = pickle.load(f)
    print(loaded["users"][0].name)  # Alice
```

注意：pickle 反序列化可以执行任意代码，不要加载不可信的 pickle 数据。

## 6. 如何使用 YAML 和 TOML？

YAML 和 TOML 是常用的配置文件格式：

::: code-group

```python [YAML]
import yaml  # 需要安装：pip install pyyaml

# 读取 YAML
with open("config.yaml", "r", encoding="utf-8") as f:
    config = yaml.safe_load(f)

# 写入 YAML
data = {"database": {"host": "localhost", "port": 5432}}
with open("config.yaml", "w", encoding="utf-8") as f:
    yaml.dump(data, f, allow_unicode=True, default_flow_style=False)
```

```python [TOML]
import tomllib  # Python 3.11+ 内置

# 读取 TOML
with open("config.toml", "rb") as f:
    config = tomllib.load(f)

print(config)

# 写入 TOML 需要第三方库
import tomli_w  # pip install tomli-w

data = {"project": {"name": "myapp", "version": "1.0.0"}}
with open("config.toml", "wb") as f:
    tomli_w.dump(data, f)
```

:::
