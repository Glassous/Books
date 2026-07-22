# 变量作用域

变量的作用域（Scope）决定了变量在哪些位置可以被访问。Python 遵循 LEGB 规则。

## 局部作用域

函数内部定义的变量为局部变量，仅在函数内有效：

```python
def my_func():
    x = 10  # 局部变量
    print(x)

my_func()  # 10
# print(x)  # NameError: name 'x' is not defined
```

## 全局作用域

在函数外部定义的变量为全局变量：

```python
x = 10  # 全局变量

def show():
    print(x)  # 可以访问全局变量

show()    # 10
print(x)  # 10（函数外也可以访问）
```

## global 关键字

在函数内部修改全局变量需要使用 `global`：

```python
count = 0

def increment():
    global count
    count += 1

increment()
increment()
print(count)  # 2

# 不使用 global 会创建局部变量
def wrong_increment():
    count = count + 1  # UnboundLocalError
```

## LEGB 规则

Python 按以下顺序查找变量：

1. **L**ocal（局部）
2. **E**nclosing（闭包）
3. **G**lobal（全局）
4. **B**uilt-in（内置）

```python
x = "global"  # G

def outer():
    x = "enclosing"  # E

    def inner():
        x = "local"  # L
        print(x)

    inner()

outer()  # local
```

## nonlocal 关键字

在嵌套函数中修改外部函数的变量使用 `nonlocal`：

```python
def outer():
    count = 0

    def inner():
        nonlocal count
        count += 1
        return count

    return inner

counter = outer()
print(counter())  # 1
print(counter())  # 2
print(counter())  # 3
```

## 作用域最佳实践

### 避免修改全局变量

```python
# 不推荐
total = 0

def add_to_total(x):
    global total
    total += x

# 推荐
def calculate_total(items):
    total = 0
    for x in items:
        total += x
    return total
```

### 使用返回值替代全局变量

```python
# 推荐做法
def create_counter():
    count = 0

    def counter():
        nonlocal count
        count += 1
        return count

    return counter

my_counter = create_counter()
print(my_counter())  # 1
print(my_counter())  # 2
```

### 变量查找顺序示例

```python
print(len)  # <built-in function len>（内置函数）

len = "自定义"  # 覆盖了内置函数
print(len)  # 自定义（现在查找的是全局变量）

# 避免覆盖内置函数名
```
