# 字典（dict）介绍

字典是 Python 中用于存储键值对的映射类型容器。

## 什么是字典

字典是**无序**（Python 3.7+ 有序）、**可变**的键值对集合，基于哈希表实现。

```python
# 空字典
empty = {}

# 基本字典
person = {"name": "Alice", "age": 25, "city": "Beijing"}

# 字典推导式
squares = {x: x**2 for x in range(5)}
```

## 字典的特点

### 键值对映射
```python
student = {
    "name": "Alice",
    "age": 25,
    "grade": "A"
}

# 通过键访问值
print(student["name"])   # Alice
print(student["age"])    # 25
```

### 键的唯一性
```python
d = {"a": 1, "b": 2, "a": 3}  # 重复键会覆盖
print(d)  # {'a': 3, 'b': 2}
```

### 键的要求
```python
# 键必须是可哈希的
d = {
    1: "整数键",
    "name": "字符串键",
    (1, 2): "元组键",
    True: "布尔键",
    3.14: "浮点数键"
}

# 列表不能作为键
# d = {[1, 2]: "data"}  # TypeError
```

## 字典 vs 列表

```python
# 列表：通过索引访问（整数位置）
students_list = ["Alice", "Bob", "Charlie"]
print(students_list[0])  # Alice

# 字典：通过键访问（有意义的标签）
students_dict = {
    "S001": "Alice",
    "S002": "Bob",
    "S003": "Charlie"
}
print(students_dict["S001"])  # Alice
```

## 字典的用途

### 存储结构化数据
```python
# 用户信息
user = {
    "id": 1001,
    "username": "alice",
    "email": "alice@example.com",
    "roles": ["admin", "editor"],
    "settings": {
        "theme": "dark",
        "language": "zh-CN"
    }
}
```

### 计数器
```python
from collections import Counter

# 使用字典计数
text = "hello world"
letter_count = {}
for char in text:
    letter_count[char] = letter_count.get(char, 0) + 1

# 或使用 Counter
counter = Counter(text)
```

### 映射表
```python
# 状态码映射
status_codes = {
    200: "成功",
    301: "重定向",
    404: "未找到",
    500: "服务器错误"
}
```

### 缓存
```python
cache = {}
def expensive_function(n):
    if n in cache:
        return cache[n]
    result = n ** n
    cache[n] = result
    return result
```

## 创建字典

```python
# 花括号
d1 = {"a": 1, "b": 2}

# dict() 构造函数
d2 = dict(a=1, b=2)           # {'a': 1, 'b': 2}
d3 = dict([("a", 1), ("b", 2)]) # {'a': 1, 'b': 2}
d4 = dict(zip(["a", "b"], [1, 2]))

# fromkeys()
d5 = dict.fromkeys(["a", "b", "c"], 0)
print(d5)  # {'a': 0, 'b': 0, 'c': 0}

# 字典推导式
d6 = {x: x**2 for x in range(5)}
print(d6)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```
