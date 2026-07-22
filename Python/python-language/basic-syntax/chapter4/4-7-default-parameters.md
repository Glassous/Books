# 默认参数

默认参数允许在函数定义时为参数提供默认值，调用时可不传该参数。

## 基本用法

```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")           # Hello, Alice!
greet("Bob", "Hi")       # Hi, Bob!
greet("Charlie", greeting="Hey")  # Hey, Charlie!
```

## 多个默认参数

```python
def create_profile(name, age=18, city="未知"):
    print(f"{name}, {age}岁, 来自{city}")

create_profile("Alice")           # Alice, 18岁, 来自未知
create_profile("Bob", 25)         # Bob, 25岁, 来自未知
create_profile("Charlie", city="上海")  # Charlie, 18岁, 来自上海
```

## 默认参数的求值时机

默认参数在**函数定义时**求值，而非调用时：

```python
import datetime

def log(message, timestamp=datetime.datetime.now()):
    print(f"[{timestamp}] {message}")

log("第一次调用")
log("第二次调用")  # 时间戳和第一次相同！
```

## 可变默认参数陷阱

使用可变对象作为默认参数可能导致意外行为：

```python
def add_item(item, items=[]):
    """错误的做法"""
    items.append(item)
    return items

print(add_item(1))  # [1]
print(add_item(2))  # [1, 2]（同一个列表！）
print(add_item(3))  # [1, 2, 3]
```

## 正确做法

使用 `None` 作为默认值，内部创建新对象：

```python
def add_item(item, items=None):
    """正确的做法"""
    if items is None:
        items = []
    items.append(item)
    return items

print(add_item(1))      # [1]
print(add_item(2))      # [2]（新的列表）
print(add_item(3, [0]))  # [0, 3]（使用传入的列表）
```

## 默认参数值类型

```python
# 数值
def calculate(price, tax_rate=0.08):
    return price * (1 + tax_rate)

# 字符串
def connect(host="localhost", port="3306"):
    print(f"连接 {host}:{port}")

# 布尔值
def process(data, verbose=False):
    if verbose:
        print(f"处理: {data}")
    return data

# None（表示可选参数）
def find_user(user_id, default=None):
    users = {1: "Alice", 2: "Bob"}
    return users.get(user_id, default)
```

## 默认参数顺序

默认参数必须放在非默认参数之后：

```python
# 正确
def func(a, b, c=3, d=4):
    pass

# 错误
# def func(a=1, b, c):  # SyntaxError
#     pass
```
