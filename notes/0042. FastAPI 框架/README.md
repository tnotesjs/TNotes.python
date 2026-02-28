# [0042. FastAPI 框架](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0042.%20FastAPI%20%E6%A1%86%E6%9E%B6)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 如何创建 FastAPI 应用？](#3--如何创建-fastapi-应用)
- [4. 🤔 如何使用 Pydantic 模型？](#4--如何使用-pydantic-模型)
- [5. 🤔 FastAPI 的依赖注入怎么用？](#5--fastapi-的依赖注入怎么用)
- [6. 🤔 FastAPI 如何处理异步操作？](#6--fastapi-如何处理异步操作)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- FastAPI 特性与优势
- 路径操作与参数声明
- Pydantic 模型与数据验证
- 依赖注入系统
- 异步支持
- 自动生成的 API 文档

## 2. 🫧 评价

- todo

## 3. 🤔 如何创建 FastAPI 应用？

FastAPI 是现代、高性能的异步 Web 框架：

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello, FastAPI!"}

@app.get("/items/{item_id}")
async def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "query": q}

# 启动：uvicorn main:app --reload
```

FastAPI 的核心优势：

- 自动生成 API 文档（Swagger UI 和 ReDoc）
- 基于 Python 类型提示的请求验证
- 异步支持，性能接近 Node.js 和 Go

## 4. 🤔 如何使用 Pydantic 模型？

FastAPI 使用 Pydantic 模型进行数据验证和序列化：

```python
from fastapi import FastAPI
from pydantic import BaseModel, EmailStr, Field
from typing import Optional

app = FastAPI()

class UserCreate(BaseModel):
    name: str = Field(..., min_length=2, max_length=50)
    email: EmailStr
    age: int = Field(..., ge=0, le=150)
    bio: Optional[str] = None

class UserResponse(BaseModel):
    id: int
    name: str
    email: str

users_db = []

@app.post("/users", response_model=UserResponse)
async def create_user(user: UserCreate):
    new_user = {"id": len(users_db) + 1, **user.model_dump()}
    users_db.append(new_user)
    return new_user

@app.get("/users", response_model=list[UserResponse])
async def list_users():
    return users_db
```

请求体会自动验证，不符合要求时返回 422 错误。

## 5. 🤔 FastAPI 的依赖注入怎么用？

依赖注入是 FastAPI 的核心特性，用于处理公共逻辑：

```python
from fastapi import FastAPI, Depends, HTTPException, Header

app = FastAPI()

# 依赖函数：验证 Token
async def verify_token(authorization: str = Header(...)):
    if not authorization.startswith("Bearer "):
        raise HTTPException(status_code=401, detail="无效的 Token")
    token = authorization.split(" ")[1]
    return token

# 依赖函数：获取当前用户
async def get_current_user(token: str = Depends(verify_token)):
    # 实际项目中会查询数据库
    return {"user_id": 1, "username": "alice"}

@app.get("/profile")
async def profile(user: dict = Depends(get_current_user)):
    return {"user": user}

@app.get("/admin")
async def admin(user: dict = Depends(get_current_user)):
    return {"message": f"欢迎管理员 {user['username']}"}
```

## 6. 🤔 FastAPI 如何处理异步操作？

FastAPI 原生支持 async/await，可以高效处理异步操作：

```python
from fastapi import FastAPI
import httpx
import asyncio

app = FastAPI()

@app.get("/fetch")
async def fetch_data():
    async with httpx.AsyncClient() as client:
        response = await client.get("https://api.github.com/users/octocat")
        return response.json()

@app.get("/parallel")
async def parallel_fetch():
    async with httpx.AsyncClient() as client:
        tasks = [
            client.get("https://api.github.com/users/octocat"),
            client.get("https://api.github.com/users/torvalds"),
        ]
        responses = await asyncio.gather(*tasks)
        return [r.json()["login"] for r in responses]
```

FastAPI 支持同步和异步函数混用，同步函数会在线程池中执行：

```python
# 异步函数（推荐用于 IO 操作）
@app.get("/async")
async def async_endpoint():
    await asyncio.sleep(1)
    return {"type": "async"}

# 同步函数（用于 CPU 密集型任务）
@app.get("/sync")
def sync_endpoint():
    return {"type": "sync"}
```
