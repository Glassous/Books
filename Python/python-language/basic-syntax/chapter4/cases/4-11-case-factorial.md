# 阶乘计算

阶乘（Factorial）是递归的经典入门案例，定义：`n! = n × (n-1) × (n-2) × ... × 1`

## 递归实现

```python
def factorial(n):
    """计算 n 的阶乘（递归实现）"""
    if n < 0:
        return "负数没有阶乘"
    if n <= 1:
        return 1
    return n * factorial(n - 1)

for i in range(0, 10):
    print(f"{i}! = {factorial(i)}")
```

## 循环实现

```python
def factorial_iterative(n):
    """计算 n 的阶乘（循环实现）"""
    if n < 0:
        return "负数没有阶乘"
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

for i in range(0, 10):
    print(f"{i}! = {factorial_iterative(i)}")
```

## 性能对比

```python
import time

def factorial_recursive(n):
    if n <= 1:
        return 1
    return n * factorial_recursive(n - 1)

def factorial_iterative(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

# 测试性能
test_n = 100

start = time.time()
result_rec = factorial_recursive(test_n)
time_rec = time.time() - start

start = time.time()
result_ite = factorial_iterative(test_n)
time_ite = time.time() - start

print(f"递归: {time_rec:.6f} 秒")
print(f"循环: {time_ite:.6f} 秒")
print(f"结果一致: {result_rec == result_ite}")
```

## 使用 reduce 实现

```python
from functools import reduce

def factorial_reduce(n):
    """使用 reduce 计算阶乘"""
    if n < 0:
        return "负数没有阶乘"
    if n == 0:
        return 1
    return reduce(lambda x, y: x * y, range(1, n + 1))

print(factorial_reduce(5))   # 120
print(factorial_reduce(10))  # 3628800
```

## 大数阶乘

Python 的整数是任意精度的，可以计算很大的阶乘：

```python
def factorial_large(n):
    """计算大数阶乘"""
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

# 计算 100!（查看有多少位）
result = factorial_large(100)
print(f"100! 的位数: {len(str(result))}")
print(f"100! = {result}")
```
