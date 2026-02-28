# [0040. Flask 框架](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0040.%20Flask%20%E6%A1%86%E6%9E%B6)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 如何创建 Flask 应用？](#3--如何创建-flask-应用)
- [4. 🤔 如何用 Flask 构建 RESTful API？](#4--如何用-flask-构建-restful-api)
- [5. 🤔 Flask 的模板和蓝图怎么用？](#5--flask-的模板和蓝图怎么用)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- Flask 安装与 Hello World
- 路由与视图函数
- 请求与响应对象
- 模板渲染（Jinja2）
- 表单处理与验证
- 数据库集成（Flask-SQLAlchemy）
- 用户认证（Flask-Login）
- 蓝图与模块化

## 2. 🫧 评价

- todo

## 3. 🤔 如何创建 Flask 应用？

Flask 是一个轻量级的 Web 微框架：

```python
from flask import Flask, request, jsonify

app = Flask(__name__)

# 基本路由
@app.route("/")
def index():
    return "<h1>欢迎使用 Flask</h1>"

# 带参数的路由
@app.route("/user/<username>")
def user_profile(username):
    return f"<h1>用户：{username}</h1>"

# 指定请求方法
@app.route("/login", methods=["GET", "POST"])
def login():
    if request.method == "POST":
        username = request.form["username"]
        return f"登录成功：{username}"
    return """
        <form method="post">
            <input name="username" placeholder="用户名">
            <button type="submit">登录</button>
        </form>
    """

if __name__ == "__main__":
    app.run(debug=True)
```

## 4. 🤔 如何用 Flask 构建 RESTful API？

```python
from flask import Flask, request, jsonify

app = Flask(__name__)

# 模拟数据库
todos = [
    {"id": 1, "title": "学习 Python", "done": False},
    {"id": 2, "title": "学习 Flask", "done": False},
]

# 获取所有待办事项
@app.route("/api/todos", methods=["GET"])
def get_todos():
    return jsonify(todos)

# 获取单个待办事项
@app.route("/api/todos/<int:todo_id>", methods=["GET"])
def get_todo(todo_id):
    todo = next((t for t in todos if t["id"] == todo_id), None)
    if todo:
        return jsonify(todo)
    return jsonify({"error": "未找到"}), 404

# 创建待办事项
@app.route("/api/todos", methods=["POST"])
def create_todo():
    data = request.get_json()
    todo = {
        "id": len(todos) + 1,
        "title": data["title"],
        "done": False,
    }
    todos.append(todo)
    return jsonify(todo), 201

# 更新待办事项
@app.route("/api/todos/<int:todo_id>", methods=["PUT"])
def update_todo(todo_id):
    todo = next((t for t in todos if t["id"] == todo_id), None)
    if not todo:
        return jsonify({"error": "未找到"}), 404
    data = request.get_json()
    todo.update(data)
    return jsonify(todo)

# 删除待办事项
@app.route("/api/todos/<int:todo_id>", methods=["DELETE"])
def delete_todo(todo_id):
    global todos
    todos = [t for t in todos if t["id"] != todo_id]
    return "", 204

if __name__ == "__main__":
    app.run(debug=True)
```

## 5. 🤔 Flask 的模板和蓝图怎么用？

Jinja2 模板用于渲染 HTML 页面，蓝图用于组织路由：

::: code-group

```python [模板渲染]
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/hello/<name>")
def hello(name):
    return render_template("hello.html", name=name)

# templates/hello.html 文件内容：
# <h1>你好，{{ name }}！</h1>
# {% if name == "admin" %}
#   <p>欢迎管理员</p>
# {% endif %}
```

```python [蓝图]
from flask import Flask, Blueprint

# 创建蓝图
auth_bp = Blueprint("auth", __name__, url_prefix="/auth")

@auth_bp.route("/login")
def login():
    return "登录页面"

@auth_bp.route("/register")
def register():
    return "注册页面"

# 在应用中注册蓝图
app = Flask(__name__)
app.register_blueprint(auth_bp)
# 访问 /auth/login 和 /auth/register
```

:::
