# 装饰器

装饰器（Decorator）是一种在不修改原函数代码的情况下，给函数添加额外功能的方式。

## 基本概念

```python
def decorator(func):
    def wrapper():
        print("调用前")
        func()
        print("调用后")
    return wrapper

def say_hello():
    print("Hello!")

say_hello = decorator(say_hello)
say_hello()
# 调用前
# Hello!
# 调用后
```

## @ 语法糖

```python
def decorator(func):
    def wrapper():
        print("调用前")
        func()
        print("调用后")
    return wrapper

@decorator
def say_hello():
    print("Hello!")

say_hello()
```

## 带参数和返回值的装饰器

```python
def log(func):
    def wrapper(*args, **kwargs):
        print(f"调用 {func.__name__}({args}, {kwargs})")
        result = func(*args, **kwargs)
        print(f"返回 {result}")
        return result
    return wrapper

@log
def add(a, b):
    return a + b

@log
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

print(add(3, 5))
# 调用 add((3, 5), {})
# 返回 8
# 8

print(greet("Alice", greeting="Hi"))
```

## 保留元数据

```python
import functools

def log(func):
    @functools.wraps(func)  # 保留原函数信息
    def wrapper(*args, **kwargs):
        print(f"调用 {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@log
def add(a, b):
    """两数相加"""
    return a + b

print(add.__name__)  # add（不加 wraps 会变成 wrapper）
print(add.__doc__)   # 两数相加
```

## 带参数的装饰器

```python
import functools

def repeat(n):
    """重复执行 n 次"""
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(n):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def say(message):
    print(message)

say("Hello!")
# Hello!
# Hello!
# Hello!
```

## 多个装饰器

```python
import functools

def bold(func):
    @functools.wraps(func)
    def wrapper():
        return f"<b>{func()}</b>"
    return wrapper

def italic(func):
    @functools.wraps(func)
    def wrapper():
        return f"<i>{func()}</i>"
    return wrapper

@bold
@italic
def hello():
    return "Hello"

print(hello())  # <b><i>Hello</i></b>
# 执行顺序：先应用 italic，再应用 bold
```

## 实用装饰器示例

### 计时装饰器

```python
import functools
import time

def timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        elapsed = time.time() - start
        print(f"{func.__name__} 耗时: {elapsed:.4f} 秒")
        return result
    return wrapper

@timer
def slow_function():
    sum(range(10_000_000))

slow_function()
```

### 重试装饰器

```python
import functools
import random

def retry(max_attempts=3):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise
                    print(f"第 {attempt + 1} 次失败，重试...")
            return None
        return wrapper
    return decorator

@retry(max_attempts=5)
def unstable_network_call():
    if random.random() < 0.7:
        raise ConnectionError("网络错误")
    return "成功！"

print(unstable_network_call())
```

### 权限检查装饰器

```python
import functools

def require_permission(permission):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(user, *args, **kwargs):
            if permission not in user.get("permissions", []):
                raise PermissionError(f"需要 {permission} 权限")
            return func(user, *args, **kwargs)
        return wrapper
    return decorator

@require_permission("delete")
def delete_user(user, user_id):
    return f"删除用户 {user_id}"

admin = {"name": "Alice", "permissions": ["read", "write", "delete"]}
viewer = {"name": "Bob", "permissions": ["read"]}

print(delete_user(admin, 1))  # 删除用户 1
# print(delete_user(viewer, 2))  # PermissionError
```
