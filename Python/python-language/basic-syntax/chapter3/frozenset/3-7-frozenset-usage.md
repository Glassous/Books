# frozenset 用法详解

## 集合运算

`frozenset` 支持所有集合运算（返回 frozenset）：

```python
a = frozenset([1, 2, 3, 4])
b = frozenset([3, 4, 5, 6])

# 并集
print(a | b)  # frozenset({1, 2, 3, 4, 5, 6})

# 交集
print(a & b)  # frozenset({3, 4})

# 差集
print(a - b)  # frozenset({1, 2})
print(b - a)  # frozenset({5, 6})

# 对称差集
print(a ^ b)  # frozenset({1, 2, 5, 6})
```

## 成员检测

```python
fs = frozenset(["apple", "banana", "cherry"])
print("apple" in fs)      # True
print("grape" not in fs)  # True
```

## 遍历

```python
fs = frozenset([3, 1, 4, 1, 5])
for item in fs:
    print(item, end=" ")  # 1 3 4 5（无序）
print()
```

## 作为缓存的键

```python
# 使用 frozenset 作为函数参数缓存
cache = {}

def process_numbers(numbers):
    key = frozenset(numbers)
    if key in cache:
        return cache[key]
    result = sum(x**2 for x in numbers)
    cache[key] = result
    return result

print(process_numbers([1, 2, 3]))  # 14（计算）
print(process_numbers([3, 2, 1]))  # 14（命中缓存）
print(cache)  # {frozenset({1, 2, 3}): 14}
```
