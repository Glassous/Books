# 函数定义

函数（Function）是一段可重复使用的代码块，用于完成特定任务。使用函数可以提高代码的复用性、可读性和可维护性。

## 定义函数

使用 `def` 关键字定义函数：

```python
def greet():
    print("Hello, World!")
```

- `def`：定义函数的关键字
- `greet`：函数名，遵循标识符命名规则
- `()`：放置参数列表
- `:`：标志函数头结束
- 缩进部分：函数体

## 调用函数

定义函数后，通过函数名加括号调用：

```python
def greet():
    print("Hello, World!")

# 调用函数
greet()  # Hello, World!
```

## 带参数的函数

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")  # Hello, Alice!
greet("Bob")    # Hello, Bob!
```

## 带返回值的函数

使用 `return` 语句返回值：

```python
def add(a, b):
    return a + b

result = add(3, 5)
print(result)  # 8
```

函数遇到 `return` 立即结束：

```python
def check_positive(x):
    if x > 0:
        return "正数"
    return "非正数"

print(check_positive(10))  # 正数
print(check_positive(-5))  # 非正数
```

## 空函数

使用 `pass` 作为占位符：

```python
def todo():
    pass  # 暂时为空，后续实现
```

## 函数命名规则

- 使用小写字母和下划线（snake_case）
- 名称应体现函数功能
- 避免使用关键字

```python
# 好的命名
def calculate_average():
    pass

def get_user_name():
    pass

def send_email():
    pass
```

## 函数的类型

```python
def greet():
    """不带参数、无返回值"""
    print("Hello")

def add(a, b):
    """带参数、有返回值"""
    return a + b

def show_info(name, age):
    """带参数、无返回值"""
    print(f"{name} is {age} years old")

def get_pi():
    """无参数、有返回值"""
    return 3.14159
```
