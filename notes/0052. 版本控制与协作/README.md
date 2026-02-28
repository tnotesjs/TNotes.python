# [0052. 版本控制与协作](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0052.%20%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6%E4%B8%8E%E5%8D%8F%E4%BD%9C)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 Git 基本操作有哪些？](#3--git-基本操作有哪些)
- [4. 🤔 .gitignore 怎么配置？](#4--gitignore-怎么配置)
- [5. 🤔 如何进行团队协作？](#5--如何进行团队协作)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- Git 基础回顾
- GitHub/GitLab 协作流程
- 代码审查与合并请求

## 2. 🫧 评价

- todo

## 3. 🤔 Git 基本操作有哪些？

```bash
# 初始化仓库
git init

# 基本工作流
git add .                      # 添加所有文件到暂存区
git commit -m "初始提交"        # 提交
git status                     # 查看状态
git log --oneline              # 查看提交历史

# 分支操作
git branch feature/login       # 创建分支
git checkout feature/login     # 切换分支
git checkout -b feature/login  # 创建并切换
git merge feature/login        # 合并分支

# 远程操作
git remote add origin https://github.com/user/repo.git
git push -u origin main
git pull origin main
```

## 4. 🤔 .gitignore 怎么配置？

Python 项目的 .gitignore 文件：

```gitignore
# 字节码和缓存
__pycache__/
*.py[cod]
*.pyo

# 虚拟环境
venv/
.venv/
env/

# IDE
.vscode/
.idea/
*.swp

# 环境变量
.env
.env.local

# 分发文件
dist/
build/
*.egg-info/

# 测试和覆盖率
htmlcov/
.coverage
.pytest_cache/

# 操作系统
.DS_Store
Thumbs.db
```

## 5. 🤔 如何进行团队协作？

常见的 Git 工作流：

```bash
# 1. 从主分支创建功能分支
git checkout main
git pull
git checkout -b feature/user-auth

# 2. 开发并提交
git add .
git commit -m "feat: 添加用户认证功能"

# 3. 推送到远程
git push origin feature/user-auth

# 4. 创建 Pull Request 进行代码审查

# 5. 合并后删除分支
git checkout main
git pull
git branch -d feature/user-auth
```

提交信息规范（Conventional Commits）：

- feat：新功能
- fix：修复 bug
- docs：文档变更
- refactor：重构
- test：测试
- chore：构建、工具等杂项
