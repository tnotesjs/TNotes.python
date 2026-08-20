# [0048. 单元测试](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0048.%20%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 什么是单元测试？](#2-什么是单元测试)
- [3. pytest 框架怎么用？](#3-pytest-框架怎么用)
- [4. 什么是 Mock 和测试覆盖率？](#4-什么是-mock-和测试覆盖率)

<!-- endregion:toc -->

## 1. 本节内容

- unittest 框架的使用
- 测试用例的编写
- 测试夹具（setUp、tearDown）
- 断言方法
- pytest 框架简介

## 2. 什么是单元测试？

单元测试是对代码中最小可测试单元（通常是函数或方法）进行验证的测试方法。Python 内置了 unittest 模块：

```python
import unittest

def add(a, b):
    return a + b

def divide(a, b):
    if b == 0:
        raise ValueError("除数不能为零")
    return a / b

class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(1, 2), 3)
        self.assertEqual(add(-1, 1), 0)

    def test_divide(self):
        self.assertAlmostEqual(divide(10, 3), 3.333, places=3)

    def test_divide_by_zero(self):
        with self.assertRaises(ValueError):
            divide(10, 0)

if __name__ == "__main__":
    unittest.main()
```

常用断言方法：

- assertEqual(a, b)：验证 a == b
- assertTrue(x)：验证 x 为 True
- assertIn(a, b)：验证 a 在 b 中
- assertRaises(Error)：验证抛出指定异常
- assertAlmostEqual(a, b)：验证浮点数近似相等

## 3. pytest 框架怎么用？

pytest 是更简洁强大的测试框架：

```python
# test_calculator.py
import pytest

def add(a, b):
    return a + b

def divide(a, b):
    if b == 0:
        raise ValueError("除数不能为零")
    return a / b

# 简单测试（用函数而不是类）
def test_add():
    assert add(1, 2) == 3
    assert add(-1, 1) == 0

# 测试异常
def test_divide_by_zero():
    with pytest.raises(ValueError, match="除数不能为零"):
        divide(10, 0)

# 参数化测试
@pytest.mark.parametrize("a, b, expected", [
    (1, 2, 3),
    (0, 0, 0),
    (-1, -1, -2),
])
def test_add_parametrize(a, b, expected):
    assert add(a, b) == expected

# 固定装置（fixture）
@pytest.fixture
def sample_data():
    return [1, 2, 3, 4, 5]

def test_sum(sample_data):
    assert sum(sample_data) == 15

def test_len(sample_data):
    assert len(sample_data) == 5
```

运行测试：

```bash
pytest                    # 运行所有测试
pytest -v                 # 详细输出
pytest test_calculator.py # 运行指定文件
pytest -k "test_add"      # 运行匹配名称的测试
```

## 4. 什么是 Mock 和测试覆盖率？

Mock 用于模拟外部依赖，隔离测试单元：

```python
from unittest.mock import patch, MagicMock
import requests

def get_user(user_id):
    response = requests.get(f"https://api.example.com/users/{user_id}")
    return response.json()

# 使用 Mock 替代网络请求
def test_get_user():
    with patch("requests.get") as mock_get:
        mock_get.return_value.json.return_value = {
            "id": 1,
            "name": "Alice"
        }
        result = get_user(1)
        assert result["name"] == "Alice"
        mock_get.assert_called_once()
```

测试覆盖率用于衡量测试覆盖了多少代码：

```bash
# 安装
pip install pytest-cov

# 运行并统计覆盖率
pytest --cov=myproject --cov-report=html
```
