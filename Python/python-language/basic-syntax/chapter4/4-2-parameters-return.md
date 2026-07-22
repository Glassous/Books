# 函数参数与返回值

## 参数分类

### 必需参数

调用时必须以正确的顺序传递：

```python
def greet(name, greeting):
    print(f"{greeting}, {name}!")

greet("Alice", "Hello")  # Hello, Alice!
```

### 关键字参数

通过参数名指定，不依赖顺序：

```python
def introduce(name, age, city):
    print(f"{name} is {age} years old, from {city}")

introduce(city="Beijing", name="Alice", age=25)
```

### 混合使用

位置参数必须在关键字参数之前：

```python
def introduce(name, age, city):
    print(f"{name}, {age}, {city}")

introduce("Alice", city="Shanghai", age=25)
```

## 返回值

### 单个返回值

```python
def square(x):
    return x ** 2

result = square(5)
print(result)  # 25
```

### 多个返回值

返回元组，自动解包：

```python
def min_max(numbers):
    return min(numbers), max(numbers)

low, high = min_max([3, 1, 4, 1, 5])
print(f"最小值: {low}, 最大值: {high}")
```

### 无返回值

没有 `return` 或 `return` 单独使用时返回 `None`：

```python
def log(message):
    print(f"[LOG] {message}")
    # 没有 return，默认返回 None

result = log("test")
print(result)  # None

def nothing():
    return

print(nothing())  # None
```

### 提前返回

```python
def divide(a, b):
    if b == 0:
        return "除数不能为 0"
    return a / b

print(divide(10, 2))  # 5.0
print(divide(10, 0))  # 除数不能为 0
```

## 参数解包

### 序列解包

```python
def add(a, b, c):
    return a + b + c

numbers = [1, 2, 3]
print(add(*numbers))  # 6（解包列表）

numbers = (4, 5, 6)
print(add(*numbers))  # 15（解包元组）
```

### 字典解包

```python
def introduce(name, age, city):
    print(f"{name}, {age}, {city}")

info = {"name": "Alice", "age": 25, "city": "Beijing"}
introduce(**info)  # Alice, 25, Beijing
```

## 类型注解

Python 3.5+ 支持类型注解（不影响运行）：

```python
def add(a: int, b: int) -> int:
    return a + b

def greet(name: str) -> str:
    return f"Hello, {name}"

# 类型只是提示，不会强制
result = add("hello", "world")  # 仍然可以运行
print(result)  # helloworld
```
