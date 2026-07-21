# 标识符

标识符（Identifier）是用来命名变量、函数、类、模块等程序实体的名称。

## 标识符命名规则

### 基本规则

1. **字符范围**：只能包含字母（a-z, A-Z）、数字（0-9）和下划线（_）
2. **首字符**：必须以字母或下划线开头，不能以数字开头
3. **区分大小写**：`name`、`Name`、`NAME` 是不同的标识符
4. **长度限制**：理论上无长度限制，但应保持合理长度

### 合法标识符示例

```python
name = "Alice"        # 合法
_private = 10         # 合法
myVar = "hello"       # 合法
_count = 100          # 合法
MAX_SIZE = 1000       # 合法
hello2 = "world"      # 合法
```

### 非法标识符示例

```python
# 2name = "Bob"      # 错误：以数字开头
# my-var = 10        # 错误：包含连字符
# my var = "hello"   # 错误：包含空格
# @count = 100       # 错误：包含特殊字符
# class = "Python"   # 错误：使用关键字
```

## 关键字和保留字

Python 有 35 个关键字，不能用作标识符：

```python
import keyword
print(keyword.kwlist)

# 关键字列表
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await',
 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except',
 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is',
 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return',
 'try', 'while', 'with', 'yield']
```

## 内置函数和类型名

避免使用内置函数名和类型名作为标识符：

```python
# 不推荐的命名
# list = [1, 2, 3]      # 覆盖了内置 list 类型
# str = "hello"         # 覆盖了内置 str 类型
# int = 10              # 覆盖了内置 int 类型
# print = "test"        # 覆盖了内置 print 函数
# len = 100             # 覆盖了内置 len 函数
```

## 命名风格约定

### 变量和函数名

使用小写字母，单词用下划线分隔（snake_case）：

```python
user_name = "Alice"
total_count = 100

def calculate_total():
    pass

def get_user_info():
    pass
```

### 类名

使用驼峰命名法（CamelCase），首字母大写：

```python
class UserAccount:
    pass

class DatabaseConnection:
    pass

class HttpRequestHandler:
    pass
```

### 常量

全部大写，单词用下划线分隔：

```python
MAX_SIZE = 100
DATABASE_URL = "localhost:5432"
API_KEY = "abc123"
PI = 3.14159
```

### 模块和包名

使用简短的小写字母，可以使用下划线：

```python
# 模块名
import my_module
import database_helper
import utils

# 包名
# mypackage/
# data_processing/
```

### 私有属性

以单下划线开头表示私有（约定，非强制）：

```python
class MyClass:
    def __init__(self):
        self._internal = 10    # 约定私有
        self.__private = 20    # 名称修饰
```

### 特殊方法

以双下划线开头和结尾表示特殊方法（魔术方法）：

```python
class MyClass:
    def __init__(self):      # 构造方法
        pass
    
    def __str__(self):       # 字符串表示
        pass
    
    def __len__(self):       # 长度
        pass
    
    def __getitem__(self):   # 索引访问
        pass
```

## 名称修饰（Name Mangling）

以双下划线开头的属性会被自动重命名：

```python
class Parent:
    def __init__(self):
        self.__secret = 123

class Child(Parent):
    def __init__(self):
        super().__init__()
        # self.__secret 不可访问
        # 实际存储为 _Parent__secret

obj = Child()
print(obj._Parent__secret)  # 123
```

## 命名最佳实践

### 有意义的命名

```python
# 好的命名
user_age = 25
total_price = 99.99
is_valid = True

# 避免的命名
x = 25
tp = 99.99
flag = True
```

### 避免混淆

```python
# 容易混淆的命名
l = [1, 2, 3]      # 小写 L 像数字 1
O = "hello"         # 大写 O 像数字 0
I = 100             # 大写 I 像数字 1

# 推荐的命名
my_list = [1, 2, 3]
name = "hello"
count = 100
```

### 布尔变量命名

```python
# 使用 is/has/can 等前缀
is_active = True
has_permission = False
can_execute = True
should_update = False
```

## 检查标识符合法性

```python
import keyword

def is_valid_identifier(name):
    # 检查是否为关键字
    if keyword.iskeyword(name):
        return False
    # 检查命名规则
    return name.isidentifier()

# 测试
print(is_valid_identifier("my_var"))   # True
print(is_valid_identifier("2var"))     # False
print(is_valid_identifier("class"))    # False
```
