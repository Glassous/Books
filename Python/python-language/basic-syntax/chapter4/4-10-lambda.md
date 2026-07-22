# 匿名函数

匿名函数（Lambda 函数）是一种简洁的、无需定义名称的函数，适用于简单的操作。

## lambda 语法

```python
lambda 参数: 表达式

# 相当于
def 函数名(参数):
    return 表达式
```

## 基本示例

```python
# lambda 版本
add = lambda a, b: a + b
print(add(3, 5))  # 8

# 等价的常规函数
def add(a, b):
    return a + b
```

## 与内置函数配合

### sorted()

```python
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 92},
    {"name": "Charlie", "grade": 78}
]

# 按成绩排序
sorted_students = sorted(students, key=lambda s: s["grade"])
print(sorted_students)

# 按字符串长度排序
words = ["python", "java", "c", "javascript"]
sorted_words = sorted(words, key=lambda w: len(w))
print(sorted_words)  # ['c', 'java', 'python', 'javascript']
```

### map()

```python
numbers = [1, 2, 3, 4, 5]

squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# 字符串格式化
names = ["alice", "bob", "charlie"]
capitalized = list(map(lambda n: n.capitalize(), names))
print(capitalized)  # ['Alice', 'Bob', 'Charlie']
```

### filter()

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]

evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8]

# 过滤出包含字母 'p' 的单词
words = ["apple", "banana", "grape", "orange"]
has_p = list(filter(lambda w: "p" in w, words))
print(has_p)  # ['apple', 'grape']
```

## 与列表推导式对比

```python
# map + lambda
numbers = [1, 2, 3, 4, 5]
squared1 = list(map(lambda x: x ** 2, numbers))

# 列表推导式（通常更易读）
squared2 = [x ** 2 for x in numbers]

# filter + lambda
evens1 = list(filter(lambda x: x % 2 == 0, numbers))

# 列表推导式
evens2 = [x for x in numbers if x % 2 == 0]
```

## 多参数 lambda

```python
# 两个参数
add = lambda a, b: a + b
print(add(3, 5))  # 8

# 多个参数
volume = lambda l, w, h: l * w * h
print(volume(2, 3, 4))  # 24

# 带默认值
power = lambda base, exp=2: base ** exp
print(power(3))     # 9
print(power(2, 3))  # 8
```

## 局限性

- 只能包含一个表达式，不能包含语句
- 不能使用赋值（`=`）
- 不能使用循环或条件语句（但可以使用条件表达式）

```python
# 可以使用条件表达式
max_val = lambda a, b: a if a > b else b
print(max_val(10, 20))  # 20

# 但不能使用语句
# invalid = lambda x: if x > 0: return x  # SyntaxError
```

## 应用场景

```python
# 按键排序字典
data = {"apple": 3, "banana": 1, "cherry": 2}
sorted_by_value = dict(sorted(data.items(), key=lambda item: item[1]))
print(sorted_by_value)  # {'banana': 1, 'cherry': 2, 'apple': 3}

# 自定义排序规则
points = [(1, 2), (3, 1), (5, 0), (2, 3)]
sorted_points = sorted(points, key=lambda p: p[0] + p[1])
print(sorted_points)  # [(1, 2), (3, 1), (2, 3), (5, 0)]
```
