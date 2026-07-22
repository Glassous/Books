# 函数类型

在 Python 中，函数是**一等公民**，可以像普通变量一样使用。

## 函数是对象

```python
def greet(name):
    return f"Hello, {name}!"

# 查看类型
print(type(greet))  # <class 'function'>

# 赋值给变量
my_func = greet
print(my_func("Alice"))  # Hello, Alice!

# 存储在列表中
functions = [greet, str.upper, len]
print(functions[0]("Bob"))  # Hello, Bob!
```

## 函数作为参数

函数可以传递给另一个函数（回调函数）：

```python
def apply(func, value):
    """对 value 应用 func"""
    return func(value)

def double(x):
    return x * 2

def square(x):
    return x * x

print(apply(double, 5))   # 10
print(apply(square, 5))   # 25
```

## 函数作为返回值

函数可以返回另一个函数：

```python
def make_multiplier(n):
    """返回一个乘以 n 的函数"""
    def multiplier(x):
        return x * n
    return multiplier

double = make_multiplier(2)
triple = make_multiplier(3)

print(double(5))   # 10
print(triple(5))   # 15
```

## 高阶函数

接收函数作为参数或返回函数的函数称为高阶函数。

### map() 函数

```python
def square(x):
    return x * x

numbers = [1, 2, 3, 4, 5]
squared = list(map(square, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# 多个可迭代对象
result = list(map(pow, [2, 3, 4], [3, 2, 1]))
print(result)  # [8, 9, 4]
```

### filter() 函数

```python
def is_even(x):
    return x % 2 == 0

numbers = [1, 2, 3, 4, 5, 6]
evens = list(filter(is_even, numbers))
print(evens)  # [2, 4, 6]
```

### sorted() 的 key 参数

```python
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 92},
    {"name": "Charlie", "grade": 78}
]

def get_grade(student):
    return student["grade"]

sorted_students = sorted(students, key=get_grade)
print(sorted_students)
# [{'name': 'Charlie', 'grade': 78}, {'name': 'Alice', 'grade': 85}, ...]
```

## 闭包

函数记住了其创建时的环境：

```python
def make_counter():
    count = 0

    def counter():
        nonlocal count
        count += 1
        return count

    return counter

c1 = make_counter()
c2 = make_counter()

print(c1())  # 1
print(c1())  # 2
print(c2())  # 1（独立的闭包）
print(c1())  # 3
```

## 回调函数示例

```python
def process_data(data, on_success, on_error):
    """处理数据，根据结果调用不同回调"""
    try:
        result = data ** 2
        on_success(f"成功: {result}")
    except Exception as e:
        on_error(f"错误: {e}")

def success_handler(msg):
    print(f"[OK] {msg}")

def error_handler(msg):
    print(f"[FAIL] {msg}")

process_data(5, success_handler, error_handler)
process_data("abc", success_handler, error_handler)
```
