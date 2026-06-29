# [0037. ORM 框架](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0037.%20ORM%20%E6%A1%86%E6%9E%B6)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. 什么是 ORM？](#3-什么是-orm)
- [4. 如何使用 SQLAlchemy？](#4-如何使用-sqlalchemy)
- [5. 如何定义模型关系？](#5-如何定义模型关系)
- [6. Peewee 和 Tortoise ORM 是什么？](#6-peewee-和-tortoise-orm-是什么)

<!-- endregion:toc -->

## 1. 本节内容

- SQLAlchemy 核心概念
- 定义模型与关系
- CRUD 操作
- 会话管理与查询

## 2. 评价

- todo

## 3. 什么是 ORM？

ORM（Object-Relational Mapping，对象关系映射）是一种将数据库表映射为 Python 类的技术，允许用面向对象的方式操作数据库，而不需要写原始 SQL。

ORM 的核心概念：

- 类对应表
- 实例对应行
- 属性对应字段

## 4. 如何使用 SQLAlchemy？

SQLAlchemy 是 Python 最流行的 ORM 框架：

```python
from sqlalchemy import create_engine, Column, Integer, String, Float
from sqlalchemy.orm import declarative_base, sessionmaker

# 创建引擎和基类
engine = create_engine("sqlite:///shop.db", echo=True)
Base = declarative_base()

# 定义模型
class Product(Base):
    __tablename__ = "products"

    id = Column(Integer, primary_key=True)
    name = Column(String(100), nullable=False)
    price = Column(Float, nullable=False)
    stock = Column(Integer, default=0)

    def __repr__(self):
        return f"Product(name='{self.name}', price={self.price})"

# 创建表
Base.metadata.create_all(engine)

# 创建会话
Session = sessionmaker(bind=engine)
session = Session()

# 添加数据
product = Product(name="笔记本", price=5999.0, stock=10)
session.add(product)
session.commit()

# 查询数据
all_products = session.query(Product).all()
print(all_products)

# 条件查询
expensive = session.query(Product).filter(Product.price > 1000).all()
print(expensive)

# 更新
product.price = 5499.0
session.commit()

# 删除
session.delete(product)
session.commit()

session.close()
```

## 5. 如何定义模型关系？

SQLAlchemy 支持定义表之间的关联关系：

```python
from sqlalchemy import Column, Integer, String, ForeignKey
from sqlalchemy.orm import relationship, declarative_base

Base = declarative_base()

class Author(Base):
    __tablename__ = "authors"
    id = Column(Integer, primary_key=True)
    name = Column(String(100), nullable=False)
    books = relationship("Book", back_populates="author")

    def __repr__(self):
        return f"Author(name='{self.name}')"

class Book(Base):
    __tablename__ = "books"
    id = Column(Integer, primary_key=True)
    title = Column(String(200), nullable=False)
    author_id = Column(Integer, ForeignKey("authors.id"))
    author = relationship("Author", back_populates="books")

    def __repr__(self):
        return f"Book(title='{self.title}')"

# 使用关联
author = Author(name="鲁迅")
author.books.append(Book(title="呼吁"))
author.books.append(Book(title="彷徂"))
session.add(author)
session.commit()

# 查询关联数据
for book in author.books:
    print(f"{author.name} 的作品：{book.title}")
```

## 6. Peewee 和 Tortoise ORM 是什么？

Peewee 是一个轻量级 ORM，语法简洁：

```python
from peewee import SqliteDatabase, Model, CharField, IntegerField

db = SqliteDatabase("peewee_demo.db")

class User(Model):
    name = CharField()
    age = IntegerField()

    class Meta:
        database = db

db.create_tables([User])

# CRUD 操作
User.create(name="Alice", age=25)
users = User.select().where(User.age > 20)
for user in users:
    print(user.name, user.age)
```

Tortoise ORM 是异步 ORM，适合配合 asyncio 和 FastAPI 使用：

```python
from tortoise import fields, models, Tortoise, run_async

class User(models.Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=100)
    age = fields.IntField()

    class Meta:
        table = "users"

async def main():
    await Tortoise.init(
        db_url="sqlite://tortoise_demo.db",
        modules={"models": ["__main__"]}
    )
    await Tortoise.generate_schemas()
    await User.create(name="Alice", age=25)
    users = await User.filter(age__gt=20)
    for user in users:
        print(user.name, user.age)

run_async(main())
```
