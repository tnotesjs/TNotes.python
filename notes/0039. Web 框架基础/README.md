# [0039. Web 框架基础](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0039.%20Web%20%E6%A1%86%E6%9E%B6%E5%9F%BA%E7%A1%80)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. Web 开发的基本概念是什么？](#3-web-开发的基本概念是什么)
- [4. WSGI 和 ASGI 是什么？](#4-wsgi-和-asgi-是什么)
- [5. 主流 Python Web 框架有哪些？](#5-主流-python-web-框架有哪些)

<!-- endregion:toc -->

## 1. 本节内容

- WSGI 协议
- 简单的 Web 服务器实现

## 2. 评价

- todo

## 3. Web 开发的基本概念是什么？

Web 开发围绕 HTTP 协议进行，客户端发送请求，服务器返回响应：

```python
# HTTP 请求的基本组成：
# 1. 请求方法：GET、POST、PUT、DELETE 等
# 2. URL 路径：请求的资源地址
# 3. 请求头：元数据信息
# 4. 请求体：POST/PUT 请求携带的数据

# HTTP 响应的基本组成：
# 1. 状态码：200 成功、404 未找到、500 服务器错误等
# 2. 响应头：Content-Type 等元数据
# 3. 响应体：HTML、JSON 等内容
```

Python Web 框架的作用是简化 Web 开发，处理 HTTP 请求解析、路由分发、模板渲染等底层工作。

## 4. WSGI 和 ASGI 是什么？

WSGI（Web Server Gateway Interface）是 Python Web 应用与 Web 服务器之间的标准接口：

```python
# 最简单的 WSGI 应用
def application(environ, start_response):
    status = "200 OK"
    headers = [("Content-Type", "text/html; charset=utf-8")]
    start_response(status, headers)
    return [b"<h1>Hello, WSGI!</h1>"]

# 使用 wsgiref 启动
from wsgiref.simple_server import make_server

server = make_server("localhost", 8080, application)
server.serve_forever()
```

ASGI（Asynchronous Server Gateway Interface）是 WSGI 的异步版本，支持 WebSocket 和异步处理：

```python
# 最简单的 ASGI 应用
async def application(scope, receive, send):
    await send({
        "type": "http.response.start",
        "status": 200,
        "headers": [(b"content-type", b"text/html")],
    })
    await send({
        "type": "http.response.body",
        "body": b"<h1>Hello, ASGI!</h1>",
    })
```

常见的 WSGI/ASGI 服务器：

- Gunicorn：WSGI 服务器，用于生产环境
- Uvicorn：ASGI 服务器，支持异步

## 5. 主流 Python Web 框架有哪些？

主流 Python Web 框架的对比：

- Flask：轻量级微框架，简单灵活，适合小型项目和 API
- Django：全功能框架，自带 ORM、Admin、认证等，适合大型项目
- FastAPI：现代异步框架，自动生成 API 文档，性能优异

```python
# Flask 示例
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello, Flask!"

# Django 示例（views.py）
from django.http import HttpResponse

def hello(request):
    return HttpResponse("Hello, Django!")

# FastAPI 示例
from fastapi import FastAPI
app = FastAPI()

@app.get("/")
async def hello():
    return {"message": "Hello, FastAPI!"}
```
