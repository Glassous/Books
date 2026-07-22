# 模块

模块（Module）是一个包含 Python 代码的文件，用于组织函数、类和变量。包（Package）是包含多个模块的目录。

## 导入模块

### import 语句

```python
import math
import random
import os

print(math.pi)           # 3.141592653589793
print(random.randint(1, 10))  # 随机整数
print(os.getcwd())       # 当前工作目录
```

### from ... import

导入模块中的特定内容：

```python
from math import pi, sqrt
from random import randint

print(pi)                # 3.141592653589793
print(sqrt(16))          # 4.0
print(randint(1, 100))   # 随机数
```

### 导入所有内容（不推荐）

```python
from math import *  # 可能引起命名冲突
```

### 别名

```python
import numpy as np
import pandas as pd
from datetime import datetime as dt

print(np.pi)
print(dt.now())
```

## if __name__ == '__main__'

每个 Python 模块都有 `__name__` 属性。直接运行脚本时值为 `'__main__'`，被导入时值为模块名：

```python
# calculator.py
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

# 仅在直接运行时执行
if __name__ == '__main__':
    print("测试计算器:")
    print(f"3 + 5 = {add(3, 5)}")
    print(f"10 - 4 = {subtract(10, 4)}")
```

```python
# main.py - 导入 calculator
import calculator

result = calculator.add(10, 20)
print(result)  # 30（不会打印测试代码）
```

## 模块搜索路径

Python 按以下顺序搜索模块：

```python
import sys

# 查看模块搜索路径
for path in sys.path:
    print(path)
# 1. 当前脚本所在目录
# 2. PYTHONPATH 环境变量
# 3. 标准库目录
# 4. site-packages（第三方包）
```

## 自定义模块

创建 `utils.py`：

```python
# utils.py
"""工具模块"""

def greet(name):
    return f"Hello, {name}"

def add(a, b):
    return a + b

PI = 3.14159

class Calculator:
    """简单计算器"""
    def multiply(self, a, b):
        return a * b
```

在另一个文件中使用：

```python
# main.py
import utils

# 或
# from utils import greet, add, PI, Calculator

print(utils.greet("Alice"))       # Hello, Alice
print(utils.add(5, 3))            # 8
print(utils.PI)                   # 3.14159

calc = utils.Calculator()
print(calc.multiply(4, 5))        # 20
```

## 包

包是一个包含 `__init__.py` 的目录，用于组织多个模块：

```
mypackage/
├── __init__.py     # 包初始化文件
├── math_ops.py     # 数学运算模块
└── str_ops.py      # 字符串操作模块
```

```python
# __init__.py
"""数学与字符串工具包"""
from .math_ops import add, multiply
from .str_ops import reverse, capitalize

__version__ = "1.0.0"
```

```python
# math_ops.py
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b
```

```python
# str_ops.py
def reverse(text):
    return text[::-1]

def capitalize(text):
    return text.upper()
```

导入包中的模块：

```python
# 方式一：导入整个模块
import mypackage.math_ops
print(mypackage.math_ops.add(3, 5))  # 8

# 方式二：导入特定函数
from mypackage.math_ops import multiply
print(multiply(4, 5))  # 20

# 方式三：通过 __init__.py 导入
import mypackage
print(mypackage.add(10, 20))     # 30
print(mypackage.reverse("hello"))  # olleh
```

### 子包

```
mypackage/
├── __init__.py
├── math_ops.py
├── str_ops.py
└── advanced/
    ├── __init__.py
    └── stats.py
```

```python
# advanced/stats.py
def mean(numbers):
    return sum(numbers) / len(numbers)

def median(numbers):
    sorted_nums = sorted(numbers)
    n = len(sorted_nums)
    mid = n // 2
    if n % 2 == 0:
        return (sorted_nums[mid - 1] + sorted_nums[mid]) / 2
    return sorted_nums[mid]
```

```python
from mypackage.advanced.stats import mean, median

data = [1, 3, 5, 7, 9, 11]
print(f"均值: {mean(data)}")
print(f"中位数: {median(data)}")
```

## 常用标准库模块

```python
import math      # 数学函数
import random    # 随机数
import datetime  # 日期时间
import os        # 操作系统接口
import sys       # 系统相关
import json      # JSON 处理
import re        # 正则表达式
import csv       # CSV 文件
import time      # 时间相关

# 示例
print(math.sqrt(25))                  # 5.0
print(random.choice(["A", "B", "C"]))  # 随机选择
print(datetime.date.today())           # 当前日期
print(os.path.exists("data.txt"))      # 文件是否存在
```

## 模块与脚本

同一文件既可作为模块导入，也可作为脚本运行：

```python
"""
calculator.py - 可同时作为模块和脚本使用
"""

def factorial(n):
    """计算阶乘"""
    if n <= 1:
        return 1
    return n * factorial(n - 1)

def fibonacci(n):
    """生成斐波那契数列"""
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a

if __name__ == '__main__':
    # 脚本模式：运行测试
    import sys
    if len(sys.argv) > 1:
        n = int(sys.argv[1])
        print(f"{n}! = {factorial(n)}")
        print(f"F({n}) = {fibonacci(n)}")
    else:
        for i in range(10):
            print(f"F({i}) = {fibonacci(i)}")
```
