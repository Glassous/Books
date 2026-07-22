# 传参方式

Python 支持多种参数传递方式，让函数的调用更加灵活。

## 位置参数

按参数定义顺序传递，是最基本的传参方式：

```python
def introduce(name, age, city):
    print(f"{name} is {age} years old, from {city}")

introduce("Alice", 25, "Beijing")
```

## 关键字参数

通过参数名指定传参，不依赖顺序：

```python
def introduce(name, age, city):
    print(f"{name} is {age} years old, from {city}")

introduce(age=25, city="Beijing", name="Alice")
```

## 混合传参

位置参数必须在前，关键字参数在后：

```python
def introduce(name, age, city):
    print(f"{name} is {age} years old, from {city}")

introduce("Alice", city="Beijing", age=25)
# introduce(name="Alice", 25, "Beijing")  # SyntaxError
```

## 仅限位置参数（Python 3.8+）

使用 `/` 分隔，之前的参数只能按位置传递：

```python
def divide(a, b, /):
    """a, b 只能按位置传递"""
    return a / b

print(divide(10, 3))   # 3.333...
# print(divide(a=10, b=3))  # TypeError
```

混合使用：

```python
def greet(name, /, greeting="Hello"):
    """name 只能按位置传递，greeting 可以按关键字传递"""
    print(f"{greeting}, {name}!")

greet("Alice")            # Hello, Alice!
greet("Bob", "Hi")        # Hi, Bob!
greet("Charlie", greeting="Hey")  # Hey, Charlie!
```

## 仅限关键字参数

使用 `*` 分隔，后面的参数只能按关键字传递：

```python
def create_user(name, *, age, city):
    """age 和 city 只能按关键字传递"""
    print(f"{name}, {age}, {city}")

create_user("Alice", age=25, city="Beijing")
# create_user("Alice", 25, "Beijing")  # TypeError
```

混合使用 `/` 和 `*`：

```python
def process(a, b, /, c, d, *, e, f):
    """
    a, b: 仅限位置参数
    c, d: 位置或关键字参数
    e, f: 仅限关键字参数
    """
    print(a, b, c, d, e, f)

process(1, 2, 3, 4, e=5, f=6)
process(1, 2, c=3, d=4, e=5, f=6)
```

## 传参方式对比

```python
def example(pos1, pos2, /, pos_or_kwd1, pos_or_kwd2, *, kwd1, kwd2):
    pass

# 允许的调用方式
example(1, 2, 3, 4, kwd1=5, kwd2=6)
example(1, 2, pos_or_kwd1=3, pos_or_kwd2=4, kwd1=5, kwd2=6)

# 不允许的调用
# example(pos1=1, pos2=2, 3, 4, kwd1=5, kwd2=6)  # pos1, pos2 不能按关键字传
# example(1, 2, 3, 4, 5, 6)  # kwd1, kwd2 必须按关键字传
```
