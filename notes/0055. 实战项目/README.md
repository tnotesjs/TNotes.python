# [0055. 实战项目](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0055.%20%E5%AE%9E%E6%88%98%E9%A1%B9%E7%9B%AE)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 如何设计一个完整的 Python 项目？](#2-如何设计一个完整的-python-项目)
- [3. 实战示例：待办事项 API](#3-实战示例待办事项-api)
- [4. 实战示例：Web 爬虫](#4-实战示例web-爬虫)

<!-- endregion:toc -->

## 1. 本节内容

- 命令行工具开发
- RESTful API 开发
- 爬虫系统实现
- 数据分析报告生成
- 自动化办公脚本

## 2. 如何设计一个完整的 Python 项目？

一个完整项目的开发流程：

1. 需求分析：明确项目目标和功能范围
2. 技术选型：选择合适的框架和工具
3. 项目初始化：搭建项目结构、配置环境
4. 迭代开发：分模块实现功能
5. 测试：编写单元测试和集成测试
6. 部署上线：配置 CI/CD 和生产环境

## 3. 实战示例：待办事项 API

使用 FastAPI 构建一个完整的 RESTful API：

::: code-group

```python [项目入口]
# main.py
from fastapi import FastAPI
from contextlib import asynccontextmanager
from database import create_tables
from routers import todo_router

@asynccontextmanager
async def lifespan(app: FastAPI):
    create_tables()
    yield

app = FastAPI(title="Todo API", lifespan=lifespan)
app.include_router(todo_router, prefix="/api")

@app.get("/")
async def root():
    return {"message": "Todo API is running"}
```

```python [数据模型]
# models.py
from pydantic import BaseModel, Field
from typing import Optional
from datetime import datetime

class TodoCreate(BaseModel):
    title: str = Field(..., min_length=1, max_length=200)
    description: Optional[str] = None

class TodoUpdate(BaseModel):
    title: Optional[str] = None
    description: Optional[str] = None
    completed: Optional[bool] = None

class TodoResponse(BaseModel):
    id: int
    title: str
    description: Optional[str]
    completed: bool
    created_at: datetime
```

```python [路由处理]
# routers.py
from fastapi import APIRouter, HTTPException
from models import TodoCreate, TodoUpdate, TodoResponse

todo_router = APIRouter(tags=["todos"])
todos_db = []

@todo_router.get("/todos", response_model=list[TodoResponse])
async def list_todos(completed: bool = None):
    if completed is not None:
        return [t for t in todos_db if t["completed"] == completed]
    return todos_db

@todo_router.post("/todos", response_model=TodoResponse, status_code=201)
async def create_todo(todo: TodoCreate):
    from datetime import datetime
    new_todo = {
        "id": len(todos_db) + 1,
        "completed": False,
        "created_at": datetime.now(),
        **todo.model_dump(),
    }
    todos_db.append(new_todo)
    return new_todo

@todo_router.put("/todos/{todo_id}", response_model=TodoResponse)
async def update_todo(todo_id: int, todo: TodoUpdate):
    existing = next((t for t in todos_db if t["id"] == todo_id), None)
    if not existing:
        raise HTTPException(status_code=404, detail="未找到")
    update_data = todo.model_dump(exclude_unset=True)
    existing.update(update_data)
    return existing

@todo_router.delete("/todos/{todo_id}", status_code=204)
async def delete_todo(todo_id: int):
    global todos_db
    todos_db = [t for t in todos_db if t["id"] != todo_id]
```

:::

## 4. 实战示例：Web 爬虫

使用 requests 和 BeautifulSoup 实现简单的网页爬虫：

```python
import requests
from bs4 import BeautifulSoup  # pip install beautifulsoup4
import csv
import time

def scrape_quotes(url):
    """爬取名言网站"""
    quotes = []
    while url:
        response = requests.get(url)
        soup = BeautifulSoup(response.text, "html.parser")

        for quote in soup.select(".quote"):
            text = quote.select_one(".text").get_text()
            author = quote.select_one(".author").get_text()
            tags = [tag.get_text() for tag in quote.select(".tag")]
            quotes.append({"text": text, "author": author, "tags": tags})

        # 获取下一页链接
        next_btn = soup.select_one(".next > a")
        url = f"https://quotes.toscrape.com{next_btn['href']}" if next_btn else None
        time.sleep(1)  # 礼貌爬取，避免过快请求

    return quotes

# 保存到 CSV
def save_to_csv(quotes, filename="quotes.csv"):
    with open(filename, "w", newline="", encoding="utf-8") as f:
        writer = csv.DictWriter(f, fieldnames=["text", "author", "tags"])
        writer.writeheader()
        writer.writerows(quotes)

if __name__ == "__main__":
    quotes = scrape_quotes("https://quotes.toscrape.com")
    save_to_csv(quotes)
    print(f"爬取了 {len(quotes)} 条名言")
```
