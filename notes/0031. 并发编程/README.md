# [0031. 并发编程](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0031.%20%E5%B9%B6%E5%8F%91%E7%BC%96%E7%A8%8B)

<!-- region:toc -->

- [1. 🎯 本节内容](#1--本节内容)
- [2. 🫧 评价](#2--评价)
- [3. 🤔 什么是多线程？](#3--什么是多线程)
- [4. 🤔 什么是多进程？](#4--什么是多进程)
- [5. 🤔 什么是异步编程 asyncio？](#5--什么是异步编程-asyncio)
- [6. 🤔 什么是线程同步与锁？](#6--什么是线程同步与锁)

<!-- endregion:toc -->

## 1. 🎯 本节内容

- 进程与线程的概念
- 多线程编程（threading 模块）
- 线程同步（锁、RLock、信号量、事件）
- 多进程编程（multiprocessing 模块）
- 进程间通信（队列、管道）
- 协程与异步编程（asyncio 基础）
- GIL（全局解释器锁）的影响

## 2. 🫧 评价

- todo

## 3. 🤔 什么是多线程？

多线程是指在同一进程中运行多个线程，共享进程的内存空间。Python 使用 threading 模块来实现：

```python
import threading
import time

def download(filename):
    print(f"开始下载：{filename}")
    time.sleep(2)  # 模拟下载
    print(f"下载完成：{filename}")

# 创建线程
t1 = threading.Thread(target=download, args=("file1.zip",))
t2 = threading.Thread(target=download, args=("file2.zip",))

# 启动线程
t1.start()
t2.start()

# 等待线程完成
t1.join()
t2.join()

print("所有下载完成")
```

由于 GIL（全局解释器锁）的存在，Python 的多线程不能充分利用多核 CPU 进行计算密集型任务，但对 IO 密集型任务（网络请求、文件读写）很有效。

## 4. 🤔 什么是多进程？

多进程可以绕过 GIL 限制，充分利用多核 CPU：

```python
from multiprocessing import Process, Pool
import os

def compute(n):
    print(f"进程 {os.getpid()} 开始计算")
    result = sum(range(n))
    print(f"进程 {os.getpid()} 完成：{result}")
    return result

if __name__ == "__main__":
    # 使用进程池
    with Pool(4) as pool:
        results = pool.map(compute, [10000000, 20000000, 30000000])
        print(f"结果：{results}")
```

多线程和多进程的区别：

- 多线程：共享内存，适合 IO 密集型任务，受 GIL 限制
- 多进程：独立内存，适合计算密集型任务，不受 GIL 限制

## 5. 🤔 什么是异步编程 asyncio？

asyncio 是 Python 的异步 IO 框架，使用协程实现并发，效率比多线程更高：

```python
import asyncio

async def fetch_data(url, delay):
    print(f"开始获取：{url}")
    await asyncio.sleep(delay)  # 模拟网络请求
    print(f"完成获取：{url}")
    return f"{url} 的数据"

async def main():
    # 并发执行多个协程
    tasks = [
        fetch_data("https://api1.example.com", 2),
        fetch_data("https://api2.example.com", 1),
        fetch_data("https://api3.example.com", 3),
    ]
    results = await asyncio.gather(*tasks)
    print(f"所有结果：{results}")

asyncio.run(main())
```

用 async def 定义协程函数，用 await 等待异步操作，用 asyncio.gather() 并发执行多个协程。

## 6. 🤔 什么是线程同步与锁？

当多个线程访问共享资源时，需要用锁来避免竞态条件：

```python
import threading

class BankAccount:
    def __init__(self, balance):
        self.balance = balance
        self.lock = threading.Lock()

    def withdraw(self, amount):
        with self.lock:  # 加锁
            if self.balance >= amount:
                self.balance -= amount
                return True
            return False

    def deposit(self, amount):
        with self.lock:
            self.balance += amount

account = BankAccount(1000)

def transfer(amount):
    for _ in range(100):
        account.withdraw(amount)
        account.deposit(amount)

# 多线程并发操作
threads = [threading.Thread(target=transfer, args=(10,)) for _ in range(10)]
for t in threads:
    t.start()
for t in threads:
    t.join()

print(f"最终余额：{account.balance}")  # 1000（正确）
```

常用的同步原语：

- Lock：互斥锁
- RLock：可重入锁，同一线程可多次获取
- Semaphore：信号量，控制同时访问的线程数
- Event：事件通知
- Condition：条件变量
