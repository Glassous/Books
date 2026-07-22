# 元组用法详解

## 索引与切片

```python
t = (10, 20, 30, 40, 50)

# 正向索引
print(t[0])   # 10
print(t[2])   # 30

# 反向索引
print(t[-1])  # 50
print(t[-3])  # 30

# 切片
print(t[1:4])     # (20, 30, 40)
print(t[:3])      # (10, 20, 30)
print(t[2:])      # (30, 40, 50)
print(t[::2])     # (10, 30, 50)
print(t[::-1])    # (50, 40, 30, 20, 10)
```

## 解包操作

### 基本解包

```python
person = ("Alice", 25, "Beijing")
name, age, city = person
print(name)  # Alice
print(age)   # 25
print(city)  # Beijing
```

### 星号解包

```python
numbers = (1, 2, 3, 4, 5)

first, *rest = numbers
print(first)  # 1
print(rest)   # [2, 3, 4, 5]

first, *middle, last = numbers
print(first)  # 1
print(middle) # [2, 3, 4]
print(last)   # 5

*beginning, last = numbers
print(beginning)  # [1, 2, 3, 4]
print(last)       # 5
```

## 元组操作

```python
t1 = (1, 2, 3)
t2 = (4, 5, 6)

# 拼接
t3 = t1 + t2
print(t3)  # (1, 2, 3, 4, 5, 6)

# 重复
t4 = t1 * 3
print(t4)  # (1, 2, 3, 1, 2, 3, 1, 2, 3)

# 成员检查
print(2 in t1)     # True
print(10 not in t1) # True
```

## 元组方法

```python
t = (1, 2, 3, 2, 4, 2, 5)

# count() - 统计出现次数
print(t.count(2))  # 3

# index() - 查找第一个匹配
print(t.index(3))  # 2
print(t.index(2))  # 1

# index() 带范围
print(t.index(2, 2))  # 3（从索引2开始查找）
```

## 元组比较

```python
# 逐元素比较
print((1, 2, 3) < (1, 2, 4))    # True
print((1, 2) < (1, 2, 3))       # True
print(("a", "b") < ("c",))      # True
print((1, 2) == (1, 2))         # True

# 不同类型不能比较
# print((1, "a") < (2, "b"))    # TypeError in Python 3
```

## 元组遍历

```python
t = (10, 20, 30, 40, 50)

# 遍历元素
for value in t:
    print(value)

# 遍历索引
for i in range(len(t)):
    print(f"{i}: {t[i]}")

# enumerate
for i, value in enumerate(t):
    print(f"{i}: {value}")

# 遍历多个元组
names = ("Alice", "Bob", "Charlie")
ages = (25, 30, 35)
for name, age in zip(names, ages):
    print(f"{name} is {age}")
```

## 命名元组（namedtuple）

```python
from collections import namedtuple

# 创建命名元组类型
Point = namedtuple("Point", ["x", "y"])
Person = namedtuple("Person", "name age city")

# 创建实例
p = Point(10, 20)
person = Person("Alice", 25, "Beijing")

# 访问
print(p.x)          # 10
print(p.y)          # 20
print(person.name)  # Alice

# 解包
x, y = p
name, age, city = person

# 转换为字典
print(p._asdict())         # {'x': 10, 'y': 20}
print(person._asdict())    # {'name': 'Alice', 'age': 25, 'city': 'Beijing'}
```

## 元组与类型转换

```python
# 列表转元组
list_to_tuple = tuple([1, 2, 3])
print(list_to_tuple)  # (1, 2, 3)

# 元组转列表
tuple_to_list = list((1, 2, 3))
print(tuple_to_list)  # [1, 2, 3]

# 字符串转元组
str_to_tuple = tuple("hello")
print(str_to_tuple)   # ('h', 'e', 'l', 'l', 'o')

# 转换为其他类型
print(list_to_tuple == tuple(list_to_tuple))  # True
```
