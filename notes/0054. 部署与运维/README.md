# [0054. 部署与运维](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0054.%20%E9%83%A8%E7%BD%B2%E4%B8%8E%E8%BF%90%E7%BB%B4)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 如何用 Docker 部署 Python 应用？](#3--如何用-docker-部署-python-应用)
- [4. 🤔 如何配置 CI/CD？](#4--如何配置-cicd)
- [5. 🤔 生产环境部署有哪些方式？](#5--生产环境部署有哪些方式)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- 使用 Gunicorn/uWSGI 部署 Web 应用
- Nginx 配置与反向代理
- Docker 容器化部署
- 使用 Supervisor 管理进程
- 云平台部署（AWS、阿里云、Heroku）

## 2. 🫧 评价

- todo

## 3. 🤔 如何用 Docker 部署 Python 应用？

```dockerfile
# Dockerfile
FROM python:3.12-slim

WORKDIR /app

# 先复制依赖文件，利用缓存
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 复制源代码
COPY . .

EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

```yaml
# docker-compose.yml
version: '3.8'
services:
  web:
    build: .
    ports:
      - '8000:8000'
    environment:
      - DATABASE_URL=postgresql://postgres:password@db/mydb
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

```bash
# 构建和运行
docker-compose up -d
docker-compose logs -f web
docker-compose down
```

## 4. 🤔 如何配置 CI/CD？

GitHub Actions 配置示例：

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.12'
      - name: 安装依赖
        run: |
          pip install -r requirements.txt
          pip install pytest pytest-cov
      - name: 运行测试
        run: pytest --cov=src --cov-report=xml
      - name: 代码检查
        run: |
          pip install ruff
          ruff check src/
```

## 5. 🤔 生产环境部署有哪些方式？

常见的部署方式：

- 传统服务器：Gunicorn/Uvicorn + Nginx 反向代理
- 容器化：Docker + Kubernetes
- 云平台：AWS Lambda、Google Cloud Run、Vercel
- PaaS：Heroku、Railway、Render

Nginx 反向代理配置示例：

```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /static/ {
        alias /app/static/;
    }
}
```

启动生产服务器：

```bash
# Gunicorn（WSGI，适用于 Flask/Django）
gunicorn -w 4 -b 0.0.0.0:8000 app:application

# Uvicorn（ASGI，适用于 FastAPI）
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```
