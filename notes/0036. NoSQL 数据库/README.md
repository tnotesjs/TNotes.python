# [0036. NoSQL 数据库](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0036.%20NoSQL%20%E6%95%B0%E6%8D%AE%E5%BA%93)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 如何使用 MongoDB？](#3--如何使用-mongodb)
- [4. 🤔 如何使用 Redis？](#4--如何使用-redis)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- Redis 连接与操作（redis-py）
- MongoDB 连接与操作（pymongo）

## 2. 🫧 评价

- todo

## 3. 🤔 如何使用 MongoDB？

MongoDB 是最流行的文档型 NoSQL 数据库，Python 通过 pymongo 操作：

```python
from pymongo import MongoClient  # pip install pymongo

# 连接 MongoDB
client = MongoClient("mongodb://localhost:27017/")
db = client["mydb"]
collection = db["users"]

# 插入文档
user = {"name": "Alice", "age": 25, "hobbies": ["读书", "编程"]}
result = collection.insert_one(user)
print(f"插入 ID：{result.inserted_id}")

# 批量插入
users = [
    {"name": "Bob", "age": 30},
    {"name": "Charlie", "age": 28},
]
collection.insert_many(users)

# 查询
user = collection.find_one({"name": "Alice"})
print(user)

# 条件查询
for user in collection.find({"age": {"$gt": 25}}):
    print(user["name"], user["age"])

# 更新
collection.update_one(
    {"name": "Alice"},
    {"$set": {"age": 26}}
)

# 删除
collection.delete_one({"name": "Charlie"})

client.close()
```

## 4. 🤔 如何使用 Redis？

Redis 是高性能的键值对存储数据库，常用于缓存和会话管理：

```python
import redis  # pip install redis

r = redis.Redis(host="localhost", port=6379, db=0, decode_responses=True)

# 字符串操作
r.set("name", "Alice")
r.set("token", "abc123", ex=3600)  # 设置过期时间 3600 秒
print(r.get("name"))  # Alice

# 哈希操作
r.hset("user:1", mapping={"name": "Alice", "age": "25"})
print(r.hgetall("user:1"))  # {'name': 'Alice', 'age': '25'}

# 列表操作
r.rpush("queue", "task1", "task2", "task3")
print(r.lpop("queue"))  # task1
print(r.lrange("queue", 0, -1))  # ['task2', 'task3']

# 集合操作
r.sadd("tags", "python", "redis", "database")
print(r.smembers("tags"))  # {'python', 'redis', 'database'}

# 有序集合
r.zadd("ranking", {"Alice": 100, "Bob": 85, "Charlie": 92})
print(r.zrevrange("ranking", 0, -1, withscores=True))
```

MongoDB 和 Redis 的区别：

- MongoDB：文档型，用于存储复杂结构化数据，支持丰富查询
- Redis：键值型，内存存储，速度极快，适合缓存和实时数据
