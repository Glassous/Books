# 列表（list）介绍

列表是 Python 中最常用的序列类型之一，用于存储有序的可变元素集合。

## 什么是列表

列表是一种**有序**、**可变**、**可重复**的序列类型，可以存储任意类型的元素。

```python
# 空列表
empty = []

# 整数列表
numbers = [1, 2, 3, 4, 5]

# 混合类型列表
mixed = [1, "hello", 3.14, True]

# 嵌套列表
nested = [[1, 2], [3, 4], [5, 6]]
```

## 列表的特点

### 有序性
列表维护元素的插入顺序，可以通过索引访问：

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])   # apple
print(fruits[-1])  # cherry
```

### 可变性
列表可以修改、添加和删除元素：

```python
fruits = ["apple", "banana"]
fruits[0] = "avocado"      # 修改
fruits.append("cherry")    # 添加
fruits.remove("banana")    # 删除
```

### 可重复
列表可以包含重复元素：

```python
numbers = [1, 2, 2, 3, 3, 3]
```

### 元素异质性
列表可以包含不同类型：

```python
info = ["Alice", 25, 3.14, True, None, [1, 2]]
```

## 创建列表

```python
# 使用方括号
list1 = [1, 2, 3]

# 使用 list() 构造函数
list2 = list("hello")      # ['h', 'e', 'l', 'l', 'o']
list3 = list(range(5))     # [0, 1, 2, 3, 4]

# 列表推导式
squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
```

## 列表的基本操作

```python
# 长度
len([1, 2, 3])  # 3

# 拼接
[1, 2] + [3, 4]  # [1, 2, 3, 4]

# 重复
[1, 2] * 3  # [1, 2, 1, 2, 1, 2]

# 成员检查
3 in [1, 2, 3]  # True
5 not in [1, 2, 3]  # True
```

## 列表 vs 其他语言中的数组

```python
# Python 列表不同于 C/Java 数组：
# 1. 无需声明大小
# 2. 可以存储不同类型
# 3. 自动扩容

# 动态增长
numbers = []
for i in range(100):
    numbers.append(i)  # 自动扩容
```

## 列表的内存表示

```python
# 列表是对象引用数组
a = [1, 2, 3]
b = a          # 引用赋值
b.append(4)    # 修改 b 也影响 a
print(a)       # [1, 2, 3, 4]

# 创建副本
c = a.copy()
c.append(5)
print(a)       # [1, 2, 3, 4]（不受影响）
```
