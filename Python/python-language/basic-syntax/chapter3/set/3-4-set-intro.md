# 集合（set）介绍

集合是 Python 中用于存储不重复元素的无序容器类型。

## 什么是集合

集合是**无序**、**不重复**、**可变**的元素集合，基于哈希表实现。

```python
# 空集合
empty = set()

# 基本集合
fruits = {"apple", "banana", "cherry"}
numbers = {1, 2, 3, 4, 5}

# 自动去重
duplicates = {1, 2, 2, 3, 3, 3}
print(duplicates)  # {1, 2, 3}
```

## 集合的特点

### 无序性
集合不维护元素顺序：

```python
s = {3, 1, 2}
print(s)  # 可能输出 {1, 2, 3} 或 {3, 1, 2}（顺序不确定）
```

### 不重复性
集合自动去重：

```python
s = {1, 2, 2, 3, 3, 3, 4}
print(len(s))  # 4
```

### 元素要求可哈希
```python
# 可哈希的元素可以放入集合
s = {1, 3.14, "hello", (1, 2)}

# 不可哈希的元素不能放入
# s = {[1, 2]}  # TypeError: unhashable type: 'list'
```

## 集合 vs 列表

```python
# 列表：有序、可重复、可索引
list = [1, 2, 2, 3, 3, 3]
print(list[0])  # 可以通过索引访问

# 集合：无序、不重复、不可索引
set = {1, 2, 3}
# print(set[0])  # TypeError
```

## 集合的用途

### 去重

```python
numbers = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
unique = list(set(numbers))
print(unique)  # [1, 2, 3, 4]
```

### 集合运算

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

# 并集
print(a | b)  # {1, 2, 3, 4, 5, 6}

# 交集
print(a & b)  # {3, 4}

# 差集
print(a - b)  # {1, 2}

# 对称差集
print(a ^ b)  # {1, 2, 5, 6}
```

### 快速成员检查

```python
import time

# 列表成员检查 O(n)
list_data = list(range(100000))
start = time.time()
print(99999 in list_data)
print(f"列表查找: {time.time() - start:.4f}s")

# 集合成员检查 O(1)
set_data = set(range(100000))
start = time.time()
print(99999 in set_data)
print(f"集合查找: {time.time() - start:.4f}s")
```

## 创建集合

```python
# 使用花括号
s1 = {1, 2, 3}

# set() 构造函数
s2 = set([1, 2, 3])      # {1, 2, 3}
s3 = set("hello")         # {'h', 'e', 'l', 'o'}
s4 = set(range(5))        # {0, 1, 2, 3, 4}

# 集合推导式
s5 = {x**2 for x in range(5)}  # {0, 1, 4, 9, 16}
```

## 不可变集合：frozenset

```python
# frozenset 是不可变的集合
fs = frozenset([1, 2, 3])
# fs.add(4)  # AttributeError

# frozenset 可以作为字典键
cache = {frozenset([1, 2]): "data"}
```
