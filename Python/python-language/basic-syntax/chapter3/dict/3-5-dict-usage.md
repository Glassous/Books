# 字典用法详解

## 访问元素

```python
person = {"name": "Alice", "age": 25, "city": "Beijing"}

# 直接访问（键不存在则报错）
print(person["name"])  # Alice
# print(person["country"])  # KeyError

# get() - 安全访问
print(person.get("name"))      # Alice
print(person.get("country"))   # None
print(person.get("country", "未知"))  # 未知

# setdefault() - 获取或设置默认值
city = person.setdefault("city", "Shanghai")
print(city)  # Beijing（已有则不修改）
country = person.setdefault("country", "China")
print(country)  # China（新增）
```

## 添加与修改

```python
person = {"name": "Alice"}

# 添加新键值对
person["age"] = 25
print(person)  # {'name': 'Alice', 'age': 25}

# 修改已有键
person["age"] = 26
print(person)  # {'name': 'Alice', 'age': 26}

# update() - 批量添加/修改
person.update({"city": "Beijing", "age": 27})
print(person)  # {'name': 'Alice', 'age': 27, 'city': 'Beijing'}

# 使用 ** 合并
info = {"email": "alice@example.com"}
person = {**person, **info}
print(person)  # {'name': 'Alice', 'age': 27, 'city': 'Beijing', 'email': 'alice@example.com'}
```

## 删除元素

```python
person = {"name": "Alice", "age": 25, "city": "Beijing", "email": "alice@example.com"}

# pop() - 删除并返回值
age = person.pop("age")
print(age)     # 25
print(person)  # {'name': 'Alice', 'city': 'Beijing', 'email': 'alice@example.com'}

# popitem() - 删除并返回最后一个键值对
last = person.popitem()
print(last)   # ('email', 'alice@example.com')
print(person)  # {'name': 'Alice', 'city': 'Beijing'}

# del 语句
del person["city"]
print(person)  # {'name': 'Alice'}

# clear() - 清空
person.clear()
print(person)  # {}
```

## 字典遍历

```python
person = {"name": "Alice", "age": 25, "city": "Beijing"}

# 遍历键
for key in person:
    print(key)  # name, age, city

for key in person.keys():
    print(key)

# 遍历值
for value in person.values():
    print(value)  # Alice, 25, Beijing

# 遍历键值对
for key, value in person.items():
    print(f"{key}: {value}")

# 解包遍历
for item in person.items():
    key, value = item
    print(f"{key}: {value}")
```

## 成员检查

```python
person = {"name": "Alice", "age": 25, "city": "Beijing"}

# 检查键（默认行为）
print("name" in person)      # True
print("country" in person)    # False
print("Alice" in person)      # False（只检查键）

# 检查值
print("Alice" in person.values())  # True
print(25 in person.values())       # True
```

## 字典方法

```python
d = {"a": 1, "b": 2, "c": 3}

# keys() - 获取所有键
print(list(d.keys()))   # ['a', 'b', 'c']

# values() - 获取所有值
print(list(d.values()))  # [1, 2, 3]

# items() - 获取所有键值对
print(list(d.items()))   # [('a', 1), ('b', 2), ('c', 3)]

# copy() - 浅复制
d2 = d.copy()

# fromkeys() - 创建新字典
keys = ["a", "b", "c"]
d3 = dict.fromkeys(keys, 0)
print(d3)  # {'a': 0, 'b': 0, 'c': 0}
```

## 字典推导式

```python
# 基本推导式
squares = {x: x**2 for x in range(5)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# 带条件
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
print(even_squares)  # {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}

# 从两个列表创建
keys = ["name", "age", "city"]
values = ["Alice", 25, "Beijing"]
d = {k: v for k, v in zip(keys, values)}
print(d)  # {'name': 'Alice', 'age': 25, 'city': 'Beijing'}

# 转换
original = {"a": 1, "b": 2, "c": 3}
reversed_dict = {v: k for k, v in original.items()}
print(reversed_dict)  # {1: 'a', 2: 'b', 3: 'c'}
```

## 嵌套字典

```python
# 嵌套字典
company = {
    "name": "Tech Corp",
    "employees": {
        "alice": {"position": "Engineer", "salary": 80000},
        "bob": {"position": "Manager", "salary": 100000},
        "charlie": {"position": "Designer", "salary": 70000}
    },
    "location": {
        "city": "Beijing",
        "address": "123 Main St"
    }
}

# 访问嵌套值
print(company["employees"]["alice"]["position"])  # Engineer
print(company["location"]["city"])                 # Beijing
```

## defaultdict

```python
from collections import defaultdict

# 默认值为 0 的字典
count = defaultdict(int)
for char in "hello world":
    count[char] += 1
print(count)

# 默认值为列表的字典
groups = defaultdict(list)
groups["a"].append(1)
groups["a"].append(2)
groups["b"].append(3)
print(dict(groups))  # {'a': [1, 2], 'b': [3]}
```

## 字典合并

```python
d1 = {"a": 1, "b": 2}
d2 = {"c": 3, "d": 4}

# Python 3.5+
merged1 = {**d1, **d2}
print(merged1)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# Python 3.9+
merged2 = d1 | d2
print(merged2)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# update()
d1.update(d2)
print(d1)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}
```
