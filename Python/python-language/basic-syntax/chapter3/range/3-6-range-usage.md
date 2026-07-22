# range 用法详解

## 遍历

```python
# 基本遍历
for i in range(5):
    print(i, end=" ")  # 0 1 2 3 4
print()

# 指定起止
for i in range(1, 6):
    print(i, end=" ")  # 1 2 3 4 5
print()

# 带步长
for i in range(0, 10, 3):
    print(i, end=" ")  # 0 3 6 9
print()
```

## 索引遍历列表

```python
fruits = ["apple", "banana", "cherry"]
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")
```

## 倒序遍历

```python
for i in range(10, 0, -1):
    print(i, end=" ")  # 10 9 8 ... 1
print()
```

## 创建列表

```python
# 用 range 生成列表
numbers = list(range(1, 11))
print(numbers)  # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# 列表推导式
squares = [x**2 for x in range(1, 6)]
print(squares)  # [1, 4, 9, 16, 25]

# 偶数列表
evens = list(range(0, 20, 2))
print(evens)  # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```
