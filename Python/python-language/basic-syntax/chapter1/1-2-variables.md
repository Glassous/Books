# 变量

变量是存储数据的容器，在 Python 中通过赋值操作创建。

## 变量的创建

### 基本赋值

```python
name = "Alice"
age = 25
height = 1.65
is_student = True
```

### 同时赋值多个变量

```python
# 多变量同时赋值
x, y, z = 1, 2, 3

# 同一值赋给多个变量
a = b = c = 0
```

### 交换变量值

```python
a, b = 10, 20
a, b = b, a  # 交换后 a=20, b=10
```

## 变量的本质

Python 变量是对象的引用（标签），而非存储数据的容器：

```python
a = [1, 2, 3]
b = a  # b 和 a 引用同一个列表对象
b.append(4)
print(a)  # [1, 2, 3, 4]，a 也被修改了
```

### id() 查看内存地址

```python
x = 100
print(id(x))  # 查看对象的内存地址

y = x
print(id(y))  # 与 id(x) 相同

y = 200
print(id(y))  # 与 id(x) 不同，指向新对象
```

## 动态类型

Python 是动态类型语言，变量可以随时改变类型：

```python
x = 10        # int
x = "hello"   # str
x = [1, 2, 3] # list
```

### type() 查看类型

```python
x = 42
print(type(x))  # <class 'int'>

x = "hello"
print(type(x))  # <class 'str'>
```

## 变量的作用域

### 局部变量

```python
def my_func():
    local_var = 10  # 局部变量
    print(local_var)

my_func()
# print(local_var)  # NameError，函数外部无法访问
```

### 全局变量

```python
global_var = 100

def my_func():
    print(global_var)  # 可以读取全局变量

my_func()
print(global_var)
```

### global 关键字

```python
counter = 0

def increment():
    global counter  # 声明使用全局变量
    counter += 1

increment()
print(counter)  # 1
```

## 常量约定

Python 没有真正的常量，通常用全大写命名表示常量：

```python
PI = 3.14159
MAX_SIZE = 100
DATABASE_URL = "localhost:5432"
```

## 类型注解（Type Hints）

Python 3.5+ 支持类型注解，方便代码提示和静态检查：

```python
# 变量类型注解
name: str = "Alice"
age: int = 25
scores: list[int] = [90, 85, 95]

# 函数类型注解
def greet(name: str) -> str:
    return f"Hello, {name}"

# 使用 typing 模块
from typing import Optional, Union

def find_user(user_id: int) -> Optional[str]:
    if user_id == 1:
        return "Alice"
    return None
```

## del 删除变量

```python
x = 10
del x  # 删除变量
# print(x)  # NameError: name 'x' is not defined
```

## 变量命名最佳实践

```python
# 好的命名
user_name = "Alice"
total_count = 100
is_valid = True

# 避免的命名
x = "Alice"      # 含义不明确
n = 100          # 含义不明确
data = [...]     # 太笼统
```
