# 递归

递归（Recursion）是一种函数调用自身的编程技巧，用于解决可以分解为相似子问题的问题。

## 递归的要素

1. **递归出口（基准条件）**：停止递归的条件
2. **递归调用**：函数调用自身，且问题规模逐步缩小

```python
def countdown(n):
    """递归倒计时"""
    if n <= 0:          # 递归出口
        print("发射！")
        return
    print(n)
    countdown(n - 1)    # 递归调用

countdown(5)
```

## 递归执行过程

```python
def factorial(n):
    """阶乘的递归过程追踪"""
    print(f"调用 factorial({n})")
    if n <= 1:
        print(f"返回 1")
        return 1
    result = n * factorial(n - 1)
    print(f"factorial({n}) = {result}")
    return result

factorial(5)
```

## 递归 vs 循环

```python
# 循环实现
def sum_iterative(n):
    total = 0
    for i in range(1, n + 1):
        total += i
    return total

# 递归实现
def sum_recursive(n):
    if n <= 0:
        return 0
    return n + sum_recursive(n - 1)

print(sum_iterative(100))   # 5050
print(sum_recursive(100))   # 5050
```

## 递归的优缺点

### 优点
- 代码简洁，逻辑清晰
- 适合树形结构、分治算法等问题

### 缺点
- 每次调用占用栈空间
- 递归过深会导致栈溢出
- 通常比循环性能差

```python
# 递归深度限制
import sys
print(sys.getrecursionlimit())  # 默认 1000

# 设置递归深度
sys.setrecursionlimit(2000)
```

## 尾递归优化

Python 不支持尾递归优化，但了解其概念有助于写出更好的递归：

```python
# 普通递归（不是尾递归）
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)  # 乘法在递归返回后执行

# 尾递归形式（Python 不会优化）
def factorial_tail(n, acc=1):
    if n <= 1:
        return acc
    return factorial_tail(n - 1, n * acc)  # 计算在递归调用前完成
```
