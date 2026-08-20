# [0041. Django 框架](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0041.%20Django%20%E6%A1%86%E6%9E%B6)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 如何创建 Django 项目？](#2-如何创建-django-项目)
- [3. Django 的 MVT 架构是什么？](#3-django-的-mvt-架构是什么)
- [4. Django ORM 怎么用？](#4-django-orm-怎么用)
- [5. Django Admin 和中间件是什么？](#5-django-admin-和中间件是什么)

<!-- endregion:toc -->

## 1. 本节内容

- Django 安装与项目创建
- MTV 架构模式
- 模型（Model）与 ORM
- 视图（View）与 URL 配置
- 模板（Template）与模板语言
- 表单与模型表单
- 管理员后台（Admin）
- 用户认证系统
- 中间件与信号

## 2. 如何创建 Django 项目？

Django 是一个全功能的 Web 框架，提供了开箱即用的工具：

```bash
# 安装 Django
pip install django

# 创建项目
django-admin startproject myproject
cd myproject

# 创建应用
python manage.py startapp blog

# 运行开发服务器
python manage.py runserver
```

Django 项目结构：

```
myproject/
    manage.py
    myproject/
        settings.py    # 项目配置
        urls.py        # URL 路由
        wsgi.py        # WSGI 入口
    blog/
        models.py      # 数据模型
        views.py       # 视图函数
        urls.py        # 应用路由
        admin.py       # 后台管理
```

## 3. Django 的 MVT 架构是什么？

Django 采用 MVT（Model-View-Template）架构：

::: code-group

```python [Model（模型）]
# blog/models.py
from django.db import models

class Article(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    author = models.CharField(max_length=100)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title
```

```python [View（视图）]
# blog/views.py
from django.shortcuts import render
from django.http import JsonResponse
from .models import Article

def article_list(request):
    articles = Article.objects.all()
    return render(request, "blog/list.html", {"articles": articles})

def article_api(request):
    articles = list(Article.objects.values("id", "title", "author"))
    return JsonResponse(articles, safe=False)
```

```python [URL 路由]
# blog/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path("articles/", views.article_list, name="article-list"),
    path("api/articles/", views.article_api, name="article-api"),
]
```

:::

## 4. Django ORM 怎么用？

Django 自带强大的 ORM，支持丰富的数据库操作：

```python
from blog.models import Article

# 创建
article = Article.objects.create(
    title="Django 入门",
    content="Django 是一个强大的 Web 框架",
    author="Alice"
)

# 查询
all_articles = Article.objects.all()
recent = Article.objects.filter(author="Alice").order_by("-created_at")
first = Article.objects.first()

# 更新
Article.objects.filter(id=1).update(title="新标题")

# 删除
Article.objects.filter(id=1).delete()

# 复杂查询
from django.db.models import Q
articles = Article.objects.filter(
    Q(author="Alice") | Q(author="Bob")
).exclude(title__contains="草稿")
```

## 5. Django Admin 和中间件是什么？

Django Admin 提供开箱即用的后台管理界面：

```python
# blog/admin.py
from django.contrib import admin
from .models import Article

@admin.register(Article)
class ArticleAdmin(admin.ModelAdmin):
    list_display = ["title", "author", "created_at"]
    list_filter = ["author", "created_at"]
    search_fields = ["title", "content"]
```

中间件用于处理请求和响应的全局逻辑：

```python
# middleware.py
import time

class TimingMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        start = time.time()
        response = self.get_response(request)
        duration = time.time() - start
        response["X-Request-Duration"] = f"{duration:.4f}s"
        return response

# settings.py 中注册
# MIDDLEWARE = [..., 'myproject.middleware.TimingMiddleware']
```
