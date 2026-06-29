# [0049. 调试与性能分析](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0049.%20%E8%B0%83%E8%AF%95%E4%B8%8E%E6%80%A7%E8%83%BD%E5%88%86%E6%9E%90)

<!-- region:toc -->

- [1. 本节内容](#1-本节内容)
- [2. 评价](#2-评价)
- [3. Python 有哪些调试方法？](#3-python-有哪些调试方法)
- [4. 如何使用 logging 记录日志？](#4-如何使用-logging-记录日志)
- [5. 如何进行性能分析？](#5-如何进行性能分析)

<!-- endregion:toc -->

## 1. 本节内容

- 使用 pdb 进行调试
- IDE 调试技巧
- 日志记录（logging 模块）
- 性能分析（cProfile）
- 代码优化技巧

## 2. 评价

- todo

## 3. Python 有哪些调试方法？

::: code-group

```python [print 调试]
# 最简单的调试方式
def calculate(data):
    print(f"[DEBUG] 输入数据：{data}")
    result = sum(data) / len(data)
    print(f"[DEBUG] 计算结果：{result}")
    return result
```

```python [pdb 调试器]
import pdb

def buggy_function(items):
    total = 0
    for item in items:
        pdb.set_trace()  # 设置断点
        total += item["price"] * item["quantity"]
    return total

# pdb 常用命令：
# n：执行下一行
# s：进入函数
# c：继续执行
# p variable：打印变量值
# l：显示当前代码
# q：退出调试
```

```python [breakpoint 函数]
# Python 3.7+ 内置的断点函数
def process(data):
    for item in data:
        if item < 0:
            breakpoint()  # 等价于 pdb.set_trace()
        print(item)
```

:::

## 4. 如何使用 logging 记录日志？

logging 模块提供灵活的日志记录功能：

```python
import logging

# 基本配置
logging.basicConfig(
    level=logging.DEBUG,
    format="%(asctime)s [%(levelname)s] %(name)s: %(message)s",
    handlers=[
        logging.FileHandler("app.log", encoding="utf-8"),
        logging.StreamHandler(),  # 同时输出到控制台
    ]
)

logger = logging.getLogger(__name__)

def process_order(order_id):
    logger.info(f"开始处理订单：{order_id}")
    try:
        logger.debug("验证订单数据...")
        logger.info(f"订单 {order_id} 处理完成")
    except Exception as e:
        logger.error(f"订单 {order_id} 处理失败：{e}", exc_info=True)
```

日志级别：DEBUG < INFO < WARNING < ERROR < CRITICAL

## 5. 如何进行性能分析？

::: code-group

```python [timeit 计时]
import timeit

# 比较两种实现的性能
time1 = timeit.timeit(
    '[i**2 for i in range(1000)]',
    number=10000
)
time2 = timeit.timeit(
    'list(map(lambda i: i**2, range(1000)))',
    number=10000
)
print(f"列表推导：{time1:.4f} 秒")
print(f"map 函数：{time2:.4f} 秒")
```

```python [cProfile 分析器]
import cProfile

def slow_function():
    total = 0
    for i in range(100000):
        total += i ** 2
    return total

# 分析性能
cProfile.run('slow_function()')

# 或者用装饰器
def profile(func):
    import cProfile
    import pstats
    def wrapper(*args, **kwargs):
        pr = cProfile.Profile()
        pr.enable()
        result = func(*args, **kwargs)
        pr.disable()
        stats = pstats.Stats(pr)
        stats.sort_stats('cumulative')
        stats.print_stats(10)
        return result
    return wrapper
```

```python [内存分析]
# pip install memory_profiler
from memory_profiler import profile

@profile
def memory_hungry():
    big_list = [i ** 2 for i in range(1000000)]
    del big_list
    return "done"

memory_hungry()
```

:::
