# 斐波那契数列

斐波那契数列（Fibonacci Sequence）定义：`F(0) = 0, F(1) = 1, F(n) = F(n-1) + F(n-2)`

## 递归实现

```python
def fibonacci_recursive(n):
    """递归实现斐波那契（效率低）"""
    if n <= 0:
        return 0
    if n == 1:
        return 1
    return fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2)

# 打印前 10 项
for i in range(10):
    print(f"F({i}) = {fibonacci_recursive(i)}")
```

## 递归优化（记忆化）

```python
from functools import lru_cache

@lru_cache(maxsize=1000)
def fibonacci_memo(n):
    """带缓存的递归实现"""
    if n <= 0:
        return 0
    if n == 1:
        return 1
    return fibonacci_memo(n - 1) + fibonacci_memo(n - 2)

# 性能对比
import time

start = time.time()
print(f"F(35) 递归: {fibonacci_recursive(35)}", end=" ")
print(f"耗时: {time.time() - start:.4f} 秒")

start = time.time()
print(f"F(35) 记忆化: {fibonacci_memo(35)}", end=" ")
print(f"耗时: {time.time() - start:.4f} 秒")
```

## 循环实现

```python
def fibonacci_iterative(n):
    """循环实现斐波那契（最优）"""
    if n <= 0:
        return 0
    if n == 1:
        return 1

    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b

print("前 20 项:")
for i in range(20):
    print(f"F({i:2d}) = {fibonacci_iterative(i):5d}")
```

## 生成器实现

```python
def fibonacci_generator():
    """生成器实现斐波那契数列"""
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

# 取前 20 项
fib = fibonacci_generator()
for _ in range(20):
    print(next(fib), end=" ")
print()
```

## 性能对比

```python
def test_fibonacci(n):
    """测试不同实现的性能"""
    import time

    # 递归（小 n）
    if n <= 30:
        start = time.time()
        result = fibonacci_recursive(n)
        t1 = time.time() - start
    else:
        t1 = float('inf')

    # 记忆化递归
    start = time.time()
    result = fibonacci_memo(n)
    t2 = time.time() - start

    # 循环
    start = time.time()
    result = fibonacci_iterative(n)
    t3 = time.time() - start

    print(f"n={n}:")
    if t1 != float('inf'):
        print(f"  普通递归: {t1:.6f} 秒")
    else:
        print(f"  普通递归: 太慢（跳过）")
    print(f"  记忆化递归: {t2:.6f} 秒")
    print(f"  循环: {t3:.6f} 秒")
    print(f"  结果: {result}")

test_fibonacci(10)
test_fibonacci(30)
test_fibonacci(100)
```
