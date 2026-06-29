# [0035. 关系型数据库](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0035.%20%E5%85%B3%E7%B3%BB%E5%9E%8B%E6%95%B0%E6%8D%AE%E5%BA%93)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. 如何使用 SQLite？](#3-如何使用-sqlite)
- [4. 如何使用 MySQL？](#4-如何使用-mysql)
- [5. 如何使用 PostgreSQL？](#5-如何使用-postgresql)

<!-- endregion:toc -->

## 1. 本节内容

- SQLite 的使用（sqlite3 模块）
- MySQL 连接与操作（PyMySQL、mysql-connector）
- PostgreSQL 连接与操作（psycopg2）
- 连接池与 ORM 思想

## 2. 评价

- todo

## 3. 如何使用 SQLite？

SQLite 是 Python 内置的轻量级关系型数据库，无需安装额外软件：

```python
import sqlite3

# 连接数据库（文件不存在会自动创建）
conn = sqlite3.connect("example.db")
cursor = conn.cursor()

# 创建表
cursor.execute("""
    CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        email TEXT UNIQUE,
        age INTEGER
    )
""")

# 插入数据
cursor.execute(
    "INSERT INTO users (name, email, age) VALUES (?, ?, ?)",
    ("Alice", "alice@example.com", 25)
)

# 批量插入
users = [
    ("Bob", "bob@example.com", 30),
    ("Charlie", "charlie@example.com", 28),
]
cursor.executemany(
    "INSERT INTO users (name, email, age) VALUES (?, ?, ?)",
    users
)

conn.commit()

# 查询数据
cursor.execute("SELECT * FROM users WHERE age > ?", (25,))
for row in cursor.fetchall():
    print(row)

# 关闭连接
conn.close()
```

使用 with 语句自动管理事务：

```python
with sqlite3.connect("example.db") as conn:
    conn.execute("INSERT INTO users (name, email, age) VALUES (?, ?, ?)",
                 ("Dave", "dave@example.com", 35))
    # 退出 with 时自动 commit，出错则自动 rollback
```

## 4. 如何使用 MySQL？

使用 pymysql 或 mysql-connector-python 操作 MySQL 数据库：

```python
import pymysql  # pip install pymysql

# 连接数据库
conn = pymysql.connect(
    host="localhost",
    user="root",
    password="password",
    database="mydb",
    charset="utf8mb4"
)

try:
    with conn.cursor() as cursor:
        # 创建表
        cursor.execute("""
            CREATE TABLE IF NOT EXISTS products (
                id INT AUTO_INCREMENT PRIMARY KEY,
                name VARCHAR(100) NOT NULL,
                price DECIMAL(10, 2)
            )
        """)

        # 插入数据
        cursor.execute(
            "INSERT INTO products (name, price) VALUES (%s, %s)",
            ("笔记本", 5999.00)
        )
        conn.commit()

        # 查询数据
        cursor.execute("SELECT * FROM products")
        for row in cursor.fetchall():
            print(row)
finally:
    conn.close()
```

## 5. 如何使用 PostgreSQL？

使用 psycopg2 操作 PostgreSQL 数据库：

```python
import psycopg2  # pip install psycopg2-binary

conn = psycopg2.connect(
    host="localhost",
    dbname="mydb",
    user="postgres",
    password="password"
)

try:
    with conn.cursor() as cur:
        cur.execute("""
            CREATE TABLE IF NOT EXISTS articles (
                id SERIAL PRIMARY KEY,
                title VARCHAR(200) NOT NULL,
                content TEXT,
                created_at TIMESTAMP DEFAULT NOW()
            )
        """)

        cur.execute(
            "INSERT INTO articles (title, content) VALUES (%s, %s) RETURNING id",
            ("第一篇文章", "文章内容...")
        )
        article_id = cur.fetchone()[0]
        print(f"插入的文章 ID：{article_id}")

        conn.commit()

        cur.execute("SELECT * FROM articles")
        for row in cur.fetchall():
            print(row)
finally:
    conn.close()
```

三种数据库的适用场景：

- SQLite：轻量级项目、原型开发、嵌入式应用
- MySQL：Web 应用、中小型项目
- PostgreSQL：复杂查询、大型项目、需要高级功能
