# [0028. 文件与 IO 操作](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0028.%20%E6%96%87%E4%BB%B6%E4%B8%8E%20IO%20%E6%93%8D%E4%BD%9C)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 如何读写文本文件？](#2-如何读写文本文件)
- [3. 如何处理二进制文件？](#3-如何处理二进制文件)
- [4. 如何操作文件路径？](#4-如何操作文件路径)
- [5. 什么是标准输入输出？](#5-什么是标准输入输出)

<!-- endregion:toc -->

## 1. 本节内容

- 打开文件（open 函数与模式）
- 读取文件（read、readline、readlines）
- 写入文件（write、writelines）
- 文件指针定位（seek、tell）
- 使用 with 语句管理文件
- 目录操作（os 模块与 pathlib 模块）

## 2. 如何读写文本文件？

使用内置的 open() 函数配合 with 语句来读写文件：

::: code-group

```python [写入文件]
# 写入文件（w 模式会覆盖原内容）
with open("output.txt", "w", encoding="utf-8") as f:
    f.write("第一行\n")
    f.write("第二行\n")

# 追加内容（a 模式）
with open("output.txt", "a", encoding="utf-8") as f:
    f.write("追加的内容\n")

# 写入多行
lines = ["第一行\n", "第二行\n", "第三行\n"]
with open("output.txt", "w", encoding="utf-8") as f:
    f.writelines(lines)
```

```python [读取文件]
# 读取整个文件
with open("output.txt", "r", encoding="utf-8") as f:
    content = f.read()
    print(content)

# 逐行读取
with open("output.txt", "r", encoding="utf-8") as f:
    for line in f:
        print(line.strip())

# 读取所有行到列表
with open("output.txt", "r", encoding="utf-8") as f:
    lines = f.readlines()
    print(lines)
```

:::

常用文件打开模式：

- r：只读（默认）
- w：写入（覆盖）
- a：追加
- x：创建（文件已存在则报错）
- b：二进制模式（如 rb、wb）
- +：读写模式（如 r+、w+）

## 3. 如何处理二进制文件？

二进制模式用于处理非文本文件，如图片、音频等：

```python
# 复制二进制文件
with open("image.png", "rb") as src:
    data = src.read()

with open("image_copy.png", "wb") as dst:
    dst.write(data)

# 分块读取大文件
def copy_file(src_path, dst_path, chunk_size=8192):
    with open(src_path, "rb") as src, open(dst_path, "wb") as dst:
        while True:
            chunk = src.read(chunk_size)
            if not chunk:
                break
            dst.write(chunk)
```

## 4. 如何操作文件路径？

pathlib 是 Python 3 推荐的文件路径处理方式：

```python
from pathlib import Path

# 创建路径对象
p = Path("./data/output")

# 常用操作
print(p.exists())       # 是否存在
print(p.is_file())      # 是否是文件
print(p.is_dir())       # 是否是目录
print(p.suffix)         # 文件后缀
print(p.stem)           # 文件名（不含后缀）
print(p.parent)         # 父目录
print(p.name)           # 文件名

# 拼接路径
config_path = Path.home() / ".config" / "app" / "settings.json"

# 创建目录
Path("data/subdir").mkdir(parents=True, exist_ok=True)

# 遍历目录
for f in Path(".").glob("*.py"):
    print(f)

# 递归遍历
for f in Path(".").rglob("*.txt"):
    print(f)

# 读写文件（简洁方式）
path = Path("hello.txt")
path.write_text("你好，世界", encoding="utf-8")
content = path.read_text(encoding="utf-8")
print(content)  # 你好，世界
```

## 5. 什么是标准输入输出？

Python 的标准 IO 包括 stdin、stdout 和 stderr：

```python
import sys

# 标准输出
sys.stdout.write("输出到控制台\n")
print("等价于 sys.stdout.write")

# 标准错误
sys.stderr.write("错误信息\n")

# 标准输入
data = input("请输入：")  # 等价于从 sys.stdin 读取

# 重定向输出到文件
with open("log.txt", "w") as f:
    print("这会写入文件", file=f)

# 使用 io.StringIO 进行内存中的 IO
from io import StringIO

buffer = StringIO()
buffer.write("内存中的数据")
print(buffer.getvalue())  # 内存中的数据
```
