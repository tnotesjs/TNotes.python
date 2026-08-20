# [0032. 网络编程](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0032.%20%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 什么是 Socket 编程？](#2-什么是-socket-编程)
- [3. 如何发送 HTTP 请求？](#3-如何发送-http-请求)
- [4. 什么是简单的 HTTP 服务器？](#4-什么是简单的-http-服务器)

<!-- endregion:toc -->

## 1. 本节内容

- Socket 编程基础
- TCP 服务器与客户端
- UDP 通信
- HTTP 请求（urllib、requests 库）
- WebSocket 简介

## 2. 什么是 Socket 编程？

Socket（套接字）是网络通信的基础，Python 通过 socket 模块提供支持：

::: code-group

```python [服务器]
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(("127.0.0.1", 8888))
server.listen(5)
print("服务器启动，等待连接...")

while True:
    conn, addr = server.accept()
    print(f"客户端连接：{addr}")
    data = conn.recv(1024).decode("utf-8")
    print(f"收到：{data}")
    conn.send(f"服务器收到：{data}".encode("utf-8"))
    conn.close()
```

```python [客户端]
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(("127.0.0.1", 8888))
client.send("你好，服务器".encode("utf-8"))
response = client.recv(1024).decode("utf-8")
print(f"服务器响应：{response}")
client.close()
```

:::

## 3. 如何发送 HTTP 请求？

Python 有多种方式发送 HTTP 请求，最常用的是 requests 库：

```python
import requests

# GET 请求
response = requests.get("https://api.github.com/users/octocat")
print(response.status_code)  # 200
print(response.json())       # JSON 响应

# POST 请求
data = {"username": "test", "password": "123456"}
response = requests.post("https://httpbin.org/post", json=data)
print(response.json())

# 带请求头和参数
headers = {"Authorization": "Bearer token123"}
params = {"page": 1, "limit": 10}
response = requests.get(
    "https://api.example.com/data",
    headers=headers,
    params=params
)

# 下载文件
response = requests.get("https://example.com/file.zip", stream=True)
with open("file.zip", "wb") as f:
    for chunk in response.iter_content(chunk_size=8192):
        f.write(chunk)
```

使用内置的 urllib：

```python
from urllib.request import urlopen
import json

with urlopen("https://api.github.com/users/octocat") as response:
    data = json.loads(response.read().decode())
    print(data["login"])
```

## 4. 什么是简单的 HTTP 服务器？

Python 内置了简单的 HTTP 服务器，可用于开发和测试：

```python
# 命令行快速启动：
# python -m http.server 8080

# 自定义服务器
from http.server import HTTPServer, BaseHTTPRequestHandler
import json

class MyHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header("Content-Type", "application/json")
        self.end_headers()
        data = {"message": "Hello, World!", "path": self.path}
        self.wfile.write(json.dumps(data).encode())

    def do_POST(self):
        content_length = int(self.headers["Content-Length"])
        body = self.rfile.read(content_length)
        data = json.loads(body.decode())
        self.send_response(200)
        self.send_header("Content-Type", "application/json")
        self.end_headers()
        response = {"received": data}
        self.wfile.write(json.dumps(response).encode())

server = HTTPServer(("localhost", 8080), MyHandler)
print("服务器启动在 http://localhost:8080")
server.serve_forever()
```
