# [0005. 开发环境搭建](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0005.%20%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. 如何选择适合的编辑器或 IDE？](#3-如何选择适合的编辑器或-ide)
- [4. 什么是虚拟环境？如何创建和管理？](#4-什么是虚拟环境如何创建和管理)
- [5. 如何使用 pip 管理包？](#5-如何使用-pip-管理包)
- [6. 如何使用 requirements.txt 管理项目依赖？](#6-如何使用-requirementstxt-管理项目依赖)

<!-- endregion:toc -->

## 1. 本节内容

- 文本编辑器与 IDE 的选择（VS Code、PyCharm、Jupyter）
- 虚拟环境（venv、virtualenv）的创建与管理
- 包管理器 pip 的使用
- requirements.txt 与依赖管理

## 2. 评价

- todo

## 3. 如何选择适合的编辑器或 IDE？

Python 开发可以使用多种编辑器和 IDE，以下是几个主流选择：

VS Code（Visual Studio Code）：

- 微软开发的免费开源编辑器
- 通过安装 Python 扩展获得代码补全、调试、Lint 等功能
- 支持集成终端、Git、扩展生态丰富
- 轻量级，启动速度快，适合大多数开发场景

PyCharm：

- JetBrains 开发的专业 Python IDE
- 社区版免费，专业版收费
- 内置代码补全、调试器、测试工具、数据库工具
- 支持 Django、Flask 等框架的项目模板
- 功能全面但相对较重，适合大型项目开发

Jupyter Notebook：

- 基于浏览器的交互式开发环境
- 以单元格为单位编写和运行代码
- 支持实时可视化和 Markdown 文档
- 适合数据分析、机器学习、教学演示等场景

其他选择：

- Sublime Text：轻量快速的文本编辑器
- Vim/Neovim：终端编辑器，学习曲线较陡但效率极高
- Spyder：面向科学计算的 IDE，自带变量查看器和绘图窗口

## 4. 什么是虚拟环境？如何创建和管理？

虚拟环境是一个独立的 Python 运行环境，它拥有自己的 Python 解释器和第三方包。通过虚拟环境，不同项目可以使用不同版本的依赖包，避免相互冲突。

使用 venv 创建虚拟环境（Python 3 内置）：

```bash
# 创建虚拟环境
python3 -m venv myenv

# 激活虚拟环境
# macOS/Linux
source myenv/bin/activate
# Windows
myenv\Scripts\activate

# 此时终端提示符会出现 (myenv) 前缀
# 在虚拟环境中安装包只会影响当前环境
pip install requests

# 退出虚拟环境
deactivate
```

使用 virtualenv 创建虚拟环境：

```bash
# 安装 virtualenv
pip install virtualenv

# 创建虚拟环境
virtualenv myenv

# 激活和退出方式与 venv 相同
```

venv 和 virtualenv 的区别：

- venv 是 Python 3.3 以后内置的模块，无需额外安装
- virtualenv 支持 Python 2 和 Python 3，功能更丰富
- virtualenv 创建环境的速度通常更快
- 对于新项目，推荐使用 venv

## 5. 如何使用 pip 管理包？

pip 是 Python 的包管理工具，用于安装、升级和卸载第三方包。

常用命令：

```bash
# 安装包
pip install requests

# 安装指定版本
pip install requests==2.28.0

# 升级包
pip install --upgrade requests

# 卸载包
pip uninstall requests

# 查看已安装的包
pip list

# 查看某个包的详细信息
pip show requests

# 搜索包（注意：PyPI 已禁用搜索 API，建议直接在网站搜索）
# pip search requests
```

使用国内镜像源加速下载：

```bash
# 临时使用清华镜像源
pip install requests -i https://pypi.tuna.tsinghua.edu.cn/simple

# 永久设置镜像源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

## 6. 如何使用 requirements.txt 管理项目依赖？

requirements.txt 是 Python 项目中常用的依赖声明文件，记录了项目所需的所有第三方包及其版本号。

生成 requirements.txt：

```bash
# 导出当前环境中所有已安装的包
pip freeze > requirements.txt
```

生成的文件内容示例：

```txt
Flask==2.3.2
requests==2.31.0
numpy==1.24.3
```

根据 requirements.txt 安装依赖：

```bash
pip install -r requirements.txt
```

版本号的指定方式：

```txt
# 精确版本
requests==2.31.0

# 最低版本
requests>=2.28.0

# 版本范围
requests>=2.28.0,<3.0.0

# 兼容版本（相当于 >=2.28.0,<2.29.0）
requests~=2.28.0
```

推荐做法：

- 每个项目都应该在虚拟环境中开发，并维护一份 requirements.txt
- 使用精确版本号（==）可以确保团队成员使用相同的依赖版本
- 将 requirements.txt 纳入版本控制，方便团队协作和部署
