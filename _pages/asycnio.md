---
title: "asyncio"
date: "2024-05-22"
bookmark: true
thumbnail: "/assets/img/thumbnail/asyncio.webp"
---
# asyncio 教程

`asyncio` 是 Python 用于编写异步程序的库。它允许你编写单线程并发代码，通过使用 `async` 和 `await` 关键字来运行 I/O 操作而不阻塞线程。本文将介绍 `asyncio` 的基础知识、常用功能，以及如何在实际项目中使用 `asyncio`。

## 目录
1. [asyncio 基础](#asyncio-基础)
2. [定义异步函数](#定义异步函数)
3. [运行异步任务](#运行异步任务)
4. [Task 和 Future](#task-和-future)
5. [协程同步](#协程同步)
6. [常用函数](#常用函数)
7. [实际示例](#实际示例)
8. [总结](#总结)

## asyncio 基础

`asyncio` 是 Python 3.4 引入的标准库，用于实现异步编程。异步编程使得程序可以在等待 I/O 操作（如网络请求、文件读写）时执行其他任务，提高了程序的效率。

### 安装
`asyncio` 是 Python 标准库的一部分，不需要单独安装。在 Python 3.4 及以上版本中，可以直接导入使用。

```python
import asyncio
```

## 定义异步函数

使用 `async def` 关键字定义异步函数。异步函数返回一个协程对象，可以使用 `await` 关键字等待协程的完成。

```python
async def hello():
    print('Hello, world!')
```

### 使用 `await`

`await` 关键字用于等待另一个协程的完成。必须在 `async` 函数中使用 `await`。

```python
async def say_hello():
    await asyncio.sleep(1)
    print('Hello, asyncio!')
```

## 运行异步任务

### 使用 `asyncio.run()`

`asyncio.run()` 是运行主协程的便捷方法，并管理事件循环的生命周期。

```python
import asyncio

async def main():
    print('Hello, asyncio!')

asyncio.run(main())
```

### 手动管理事件循环

你也可以手动管理事件循环。

```python
import asyncio

async def main():
    print('Hello, asyncio!')

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
loop.close()
```

## Task 和 Future

### Task

`Task` 是 `Future` 的子类，表示一个异步执行的操作。使用 `asyncio.create_task()` 创建任务。

```python
import asyncio

async def say(what, when):
    await asyncio.sleep(when)
    print(what)

async def main():
    task1 = asyncio.create_task(say('Hello', 1))
    task2 = asyncio.create_task(say('World', 2))
    await task1
    await task2

asyncio.run(main())
```

### Future

`Future` 是一个低级别的对象，表示一个异步操作的结果。通常不直接使用 `Future`，而是通过 `Task` 来间接使用。

```python
import asyncio

async def set_after(fut, delay, value):
    await asyncio.sleep(delay)
    fut.set_result(value)

async def main():
    loop = asyncio.get_running_loop()
    fut = loop.create_future()
    await asyncio.create_task(set_after(fut, 1, 'Hello'))
    print(await fut)

asyncio.run(main())
```

## 协程同步

### `asyncio.gather()`

`asyncio.gather()` 可以并行运行多个协程，并收集它们的结果。

```python
import asyncio

async def say(what, when):
    await asyncio.sleep(when)
    print(what)

async def main():
    await asyncio.gather(
        say('Hello', 1),
        say('World', 2)
    )

asyncio.run(main())
```

### `asyncio.wait()`

`asyncio.wait()` 也可以并行运行多个协程，但它返回的结果不同。

```python
import asyncio

async def say(what, when):
    await asyncio.sleep(when)
    print(what)

async def main():
    tasks = [
        say('Hello', 1),
        say('World', 2)
    ]
    done, pending = await asyncio.wait(tasks)

asyncio.run(main())
```

## 常用函数

### `asyncio.sleep()`

使协程暂停一段时间。

```python
import asyncio

async def main():
    print('Start')
    await asyncio.sleep(1)
    print('End')

asyncio.run(main())
```

### `asyncio.create_task()`

创建一个并发任务。

```python
import asyncio

async def say(what, when):
    await asyncio.sleep(when)
    print(what)

async def main():
    task = asyncio.create_task(say('Hello', 1))
    await task

asyncio.run(main())
```

### `asyncio.shield()`

保护协程不被取消。

```python
import asyncio

async def worker():
    await asyncio.sleep(1)
    return 'Done'

async def main():
    task = asyncio.create_task(worker())
    result = await asyncio.shield(task)
    print(result)

asyncio.run(main())
```

## 实际示例

### 并发 HTTP 请求

使用 `aiohttp` 库实现并发 HTTP 请求。

```python
import aiohttp
import asyncio

async def fetch(session, url):
    async with session.get(url) as response:
        return await response.text()

async def main():
    async with aiohttp.ClientSession() as session:
        html = await fetch(session, 'http://python.org')
        print(html)

asyncio.run(main())
```

### 并发执行多项任务

```python
import asyncio

async def task1():
    await asyncio.sleep(1)
    print('Task 1 done')

async def task2():
    await asyncio.sleep(2)
    print('Task 2 done')

async def main():
    await asyncio.gather(task1(), task2())

asyncio.run(main())
```

## 总结

通过本文，你了解了 `asyncio` 的基础知识、如何定义和运行异步函数、任务和 Future 的使用、协程的同步方法以及常用的 `asyncio` 函数。你还学习了一些实际的使用示例，展示了如何在实际项目中应用 `asyncio`。

`asyncio` 是一个强大的工具，可以显著提高 I/O 密集型任务的性能。希望这些内容能帮助你更好地理解和使用 `asyncio`。

---

这份教程简要介绍了 `asyncio` 的基本概念和使用方法。如果你有任何问题或需要更详细的信息，请参考 [Python 官方文档](https://docs.python.org/3/library/asyncio.html) 或在社区寻求帮助。