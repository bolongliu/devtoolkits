# python 加速方法示例
Python中有几种并行处理的方法，包括多线程、多进程和异步IO。以下是每种方法的示例代码：

## 1. 使用joblib 中的 Parallel进行加速
## 2. 多线程：Python的threading模块提供了一个高级接口来管理线程。
## 3. 多进程：Python的multiprocessing模块是一个创建进程的包，它利用了Python的threading接口。
## 4. 异步IO：Python的asyncio模块提供了编写单线程并发代码的设施，使用协程，multiplexing I/O access over sockets and other resources, running network clients and servers, and other related primitives

请注意，由于Python的全局解释器锁（GIL）的存在，多线程在CPU密集型任务中可能不会提高性能。对于这种情况，多进程或异步IO可能是更好的选择。

1. 使用joblib 中的 Parallel进行加速

```python
from joblib import Parallel, delayed
import time


def single(a, b):
    """定义一个目标函数，一般是main函数"""
    time.sleep(1)
    print(a + b)


def in_loop():
    start = time.time()
    for i in range(10):
        single(i, i)
    total_time = time.time() - start
    print("loop using {} ".format(total_time))


def in_parallel():
    start = time.time()
    Parallel(n_jobs=-1)(delayed(single)(i, i) for i in range(10))  # 并行执行single函数
    total_time = time.time() - start
    print("parallel using {} ".format(total_time))


if __name__ == "__main__":
    in_loop()
    in_parallel()

```

2. 多线程：Python的threading模块提供了一个高级接口来管理线程。

```python
import threading

def worker(num):
    """thread worker function"""
    print('Worker: %s' % num)

threads = []
for i in range(5):
    t = threading.Thread(target=worker, args=(i,))
    threads.append(t)
    t.start()
```

3. 多进程：Python的multiprocessing模块是一个创建进程的包，它利用了Python的threading接口。

```python
from multiprocessing import Process

def worker(num):
    """process worker function"""
    print('Worker:', num)

if __name__ == '__main__':
    jobs = []
    for i in range(5):
        p = Process(target=worker, args=(i,))
        jobs.append(p)
        p.start()
```

4. 异步IO：Python的asyncio模块提供了编写单线程并发代码的设施，使用协程，multiplexing I/O access over sockets and other resources, running network clients and servers, and other related primitives。

```python
import asyncio

async def worker(num):
    print('Worker:', num)
    await asyncio.sleep(1)

async def main():
    tasks = [worker(i) for i in range(5)]
    await asyncio.gather(*tasks)

asyncio.run(main())
# asyncio.run()不能在已经运行的事件循环中被调用。在Jupyter notebook或IPython这样的交互式环境中，通常已经有一个运行的事件循环。
# 在Jupyter notebook或IPython中运行
await main()

```
请注意，由于Python的全局解释器锁（GIL）的存在，多线程在CPU密集型任务中可能不会提高性能。对于这种情况，多进程或异步IO可能是更好的选择。