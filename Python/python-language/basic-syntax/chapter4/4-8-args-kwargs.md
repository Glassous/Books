# 不定长参数

不定长参数允许函数接收任意数量的参数，Python 使用 `*args` 和 `**kwargs` 来实现。

## *args（位置不定长参数）

`*args` 将多余的**位置参数**打包为元组：

```python
def sum_all(*args):
    """计算所有参数的和"""
    total = 0
    for num in args:
        total += num
    return total

print(sum_all(1, 2, 3))       # 6
print(sum_all(1, 2, 3, 4, 5))  # 15
print(sum_all())               # 0
```

## **kwargs（关键字不定长参数）

`**kwargs` 将多余的**关键字参数**打包为字典：

```python
def print_info(**kwargs):
    """打印所有关键字参数"""
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25, city="Beijing")
# name: Alice
# age: 25
# city: Beijing
```

## 名称约定

`args` 和 `kwargs` 只是约定名称，`*` 和 `**` 才是关键：

```python
def example(*args, **kwargs):
    """即使换名字也能工作"""
    print(f"位置参数: {args}")
    print(f"关键字参数: {kwargs}")

example(1, 2, 3, a=4, b=5)
```

## 组合使用

```python
def func(required, *args, default="默认", **kwargs):
    print(f"必需参数: {required}")
    print(f"位置参数: {args}")
    print(f"默认参数: {default}")
    print(f"关键字参数: {kwargs}")

func(1, 2, 3, 4, default="自定义", name="Alice", age=25)
# 必需参数: 1
# 位置参数: (2, 3, 4)
# 默认参数: 自定义
# 关键字参数: {'name': 'Alice', 'age': 25}
```

参数顺序：`一般参数` -> `*args` -> `默认参数` -> `**kwargs`

## 解包传递

使用 `*` 和 `**` 将序列和字典解包后传递给函数：

```python
def introduce(name, age, city):
    print(f"{name}, {age}岁, 来自{city}")

# 列表解包
info_list = ["Alice", 25, "Beijing"]
introduce(*info_list)

# 字典解包
info_dict = {"name": "Bob", "age": 30, "city": "Shanghai"}
introduce(**info_dict)

# 混合解包
def calculate(a, b, c):
    return a * b + c

args = (2, 3)
print(calculate(*args, 4))  # 2 * 3 + 4 = 10
```

## 实际应用

### 装饰器

```python
def logger(func):
    def wrapper(*args, **kwargs):
        print(f"调用 {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@logger
def add(a, b):
    return a + b

print(add(3, 5))
```

### 安全求和

```python
def safe_sum(*args):
    """安全求和，忽略非数字参数"""
    total = 0
    for arg in args:
        if isinstance(arg, (int, float)):
            total += arg
    return total

print(safe_sum(1, 2, "a", 3, None, 4))  # 10
```

### 配置合并

```python
def connect(host, port, **options):
    """数据库连接函数"""
    config = {
        "host": host,
        "port": port,
        "timeout": 30,
        "charset": "utf8"
    }
    config.update(options)  # 用传入的参数覆盖默认值
    return config

print(connect("localhost", 3306))
print(connect("localhost", 3306, timeout=60, user="admin"))
```
