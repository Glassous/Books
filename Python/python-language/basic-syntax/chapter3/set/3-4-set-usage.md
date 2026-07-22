# 集合用法详解

## 添加与删除

```python
s = {1, 2, 3}

# add() - 添加元素
s.add(4)
print(s)  # {1, 2, 3, 4}

# add() 重复元素无效果
s.add(1)
print(s)  # {1, 2, 3, 4}

# update() - 批量添加
s.update([5, 6, 7])
print(s)  # {1, 2, 3, 4, 5, 6, 7}

# remove() - 删除元素（不存在则报错）
s.remove(7)
print(s)  # {1, 2, 3, 4, 5, 6}

# discard() - 删除元素（不存在不报错）
s.discard(10)  # 无错误
s.discard(5)
print(s)  # {1, 2, 3, 4, 6}

# pop() - 删除并返回任意元素
element = s.pop()
print(element)
print(s)

# clear() - 清空集合
s.clear()
print(s)  # set()
```

## 集合运算

### 并集

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

# 多种方式
print(a | b)            # {1, 2, 3, 4, 5, 6}
print(a.union(b))       # {1, 2, 3, 4, 5, 6}

# 更新并集
a.update(b)   # 或 a |= b
```

### 交集

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a & b)             # {3, 4}
print(a.intersection(b)) # {3, 4}

# 更新交集
a.intersection_update(b)
```

### 差集

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a - b)            # {1, 2}
print(a.difference(b))  # {1, 2}

# 更新差集
a.difference_update(b)
```

### 对称差集

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a ^ b)              # {1, 2, 5, 6}
print(a.symmetric_difference(b))  # {1, 2, 5, 6}

# 更新对称差集
a.symmetric_difference_update(b)
```

## 比较运算

```python
a = {1, 2, 3}
b = {1, 2}
c = {1, 2, 3}

# 子集
print(b.issubset(a))  # True
print({1}.issubset(a)) # True

# 超集
print(a.issuperset(b)) # True
print(a.issuperset(c)) # True

# 真子集
print(b < a)  # True
print(c < a)  # False
print(c <= a) # True

# 不相交
print({1, 2}.isdisjoint({3, 4}))  # True
print({1, 2}.isdisjoint({2, 3}))  # False
```

## 成员检查

```python
s = {1, 2, 3, 4, 5}

# in / not in
print(3 in s)      # True
print(10 in s)     # False
print(10 not in s) # True

# 集合查找比列表快得多
import time

data = list(range(1000000))
start = time.time()
999999 in data
print(f"列表查找: {time.time() - start:.6f}s")

data_set = set(data)
start = time.time()
999999 in data_set
print(f"集合查找: {time.time() - start:.6f}s")
```

## 遍历集合

```python
s = {1, 2, 3, 4, 5}

# 遍历元素（顺序不固定）
for element in s:
    print(element)

# 排序后遍历
for element in sorted(s):
    print(element)

# 转换为列表后遍历
for i, element in enumerate(sorted(s)):
    print(f"{i}: {element}")
```

## 集合推导式

```python
# 基本推导式
squares = {x**2 for x in range(10)}
print(squares)  # {0, 1, 4, 9, 16, 25, 36, 49, 64, 81}

# 带条件
even_squares = {x**2 for x in range(10) if x % 2 == 0}
print(even_squares)  # {0, 4, 16, 36, 64}

# 字符串处理
text = "hello world hello python"
unique_chars = {char for char in text if char != " "}
print(unique_chars)  # {'h', 'e', 'l', 'o', 'w', 'r', 'd', 'p', 'y', 't', 'n'}
```

## 冻结集合（frozenset）

```python
# frozenset 是不可变的
fs = frozenset([1, 2, 3])

# 支持集合运算
print(fs | {4, 5})   # frozenset({1, 2, 3, 4, 5})
print(fs & {2, 3})   # frozenset({2, 3})
print(fs - {2})      # frozenset({1, 3})

# 可哈希，可作为字典键
cache = {}
cache[frozenset([1, 2])] = "data1"
cache[frozenset([3, 4])] = "data2"
```
