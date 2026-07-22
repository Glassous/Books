# 元组（tuple）介绍

元组是 Python 中的一种有序、不可变的序列类型。

## 什么是元组

元组是**有序**、**不可变**、**可重复**的序列，一旦创建就不能修改。

```python
# 空元组
empty = ()

# 单元素元组（必须加逗号）
single = (1,)

# 多元素元组
point = (10, 20)
colors = ("red", "green", "blue")

# 省略括号
coordinates = 10, 20, 30
```

## 元组的特点

### 不可变性
```python
t = (1, 2, 3)
# t[0] = 10  # TypeError

# 但元组内包含可变对象时可修改该对象
t = ([1, 2], 3)
t[0].append(3)  # 可以，列表本身可变
print(t)  # ([1, 2, 3], 3)
```

### 有序性
```python
t = (10, 20, 30)
print(t[0])   # 10
print(t[-1])  # 30
print(t[0:2])  # (10, 20)
```

### 可哈希性
元组可以作为字典的键：

```python
# 元组可作为字典键
locations = {
    (40.7128, -74.0060): "纽约",
    (51.5074, -0.1278): "伦敦",
}
```

## 元组的用途

### 函数多返回值

```python
def min_max(numbers):
    return min(numbers), max(numbers)

result = min_max([3, 1, 4, 1, 5])
print(result)     # (1, 5)
min_val, max_val = result
```

### 保护数据不被修改

```python
# 使用元组表示常量配置
APP_CONFIG = ("localhost", 8080, "debug")
# APP_CONFIG[0] = "other"  # TypeError
```

### 作为字典键

```python
# 列表不能作为键，元组可以
cache = {}
cache[(1, 2)] = "data"  # 正确
# cache[[1, 2]] = "data"  # TypeError
```

## 元组 vs 列表

```python
# 相同点
t = (1, 2, 3)
l = [1, 2, 3]
print(t[0])     # 1
print(l[0])     # 1
print(len(t))   # 3
print(len(l))   # 3

# 不同点
# 元组不可变，列表可变
# 元组可哈希，列表不可哈希
# 元组内存占用更小
# 元组创建速度更快
```

## 创建元组

```python
# 字面量
t1 = (1, 2, 3)

# tuple() 构造函数
t2 = tuple([1, 2, 3])     # (1, 2, 3)
t3 = tuple("hello")        # ('h', 'e', 'l', 'l', 'o')
t4 = tuple(range(5))       # (0, 1, 2, 3, 4)

# 生成器表达式
t5 = tuple(x**2 for x in range(5))  # (0, 1, 4, 9, 16)
```
