# 第三章 汇总

本章汇总了 Python 八种核心数据容器的知识点，包含速览、示例代码和完整示例文件。

---

## 速览

### 3.1 列表（list）
- **特点**：有序、可变、可重复
- **创建**：`[]`、`list()`、列表推导式
- **常用**：`append()`、`insert()`、`remove()`、`pop()`、`sort()`
- **用途**：存储序列数据、栈、队列

### 3.2 字符串（str）
- **特点**：有序、不可变、Unicode
- **创建**：`''`、`""`、`""""""`
- **常用**：`split()`、`join()`、`replace()`、`strip()`、`find()`
- **用途**：文本处理、格式化、正则匹配

### 3.3 元组（tuple）
- **特点**：有序、不可变、可哈希
- **创建**：`()`、`tuple()`、省略括号
- **常用**：`count()`、`index()`、解包
- **用途**：函数多返回值、不可变数据、字典键

### 3.4 集合（set）
- **特点**：无序、不重复、可变
- **创建**：`{}`、`set()`
- **运算**：`|`（并集）、`&`（交集）、`-`（差集）、`^`（对称差）
- **用途**：去重、集合运算、快速成员检查

### 3.5 字典（dict）
- **特点**：键值对、可变、键唯一
- **创建**：`{}`、`dict()`、字典推导式
- **常用**：`get()`、`keys()`、`values()`、`items()`、`update()`
- **用途**：结构化数据、映射表、缓存、计数器

### 3.6 range
- **特点**：不可变整数序列、惰性计算
- **创建**：`range(stop)`、`range(start, stop)`、`range(start, stop, step)`
- **常用**：`for` 循环、列表生成、步进遍历
- **用途**：循环计数、数字序列、避免大列表内存占用

### 3.7 frozenset
- **特点**：不可变集合、可哈希
- **创建**：`frozenset()`、`frozenset(iterable)`
- **运算**：`|`（并集）、`&`（交集）、`-`（差集）、`^`（对称差）
- **用途**：字典键、集合元素、常量集合、缓存键

### 3.8 bytes 与 bytearray
- **特点**：`bytes` 不可变、`bytearray` 可变
- **创建**：`b"hello"`、`bytes(5)`、`bytearray(10)`
- **转换**：`encode()`、`decode()`、`.hex()`、`fromhex()`
- **用途**：二进制数据、网络通信、文件读写、加密

---

## 示例代码

### 列表操作

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("date")
fruits.insert(0, "avocado")
fruits.remove("banana")
fruits.sort()
print(fruits)
```

### 字符串操作

```python
text = "  Hello, World!  "
print(text.strip())
print(text.lower().replace("world", "Python"))
print(" ".join(["Hello", "Python"]))
```

### 元组操作

```python
point = (10, 20)
x, y = point
print(f"x={x}, y={y}")
```

### 集合操作

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
print(a | b)
print(a & b)
print(a - b)
```

### 字典操作

```python
person = {"name": "Alice", "age": 25}
print(person.get("name"))
print(person.keys())
print(person.items())
```

---

## 完整示例文件

```python
"""
第三章 数据存储容器 - 综合示例
包含：列表、字符串、元组、集合、字典
"""

# ============================================
# 1. 列表（list）
# ============================================
print("=" * 50)
print("1. 列表")
print("=" * 50)

# 创建
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
print(f"创建: {numbers}")

# 操作
numbers.append(5)
numbers.sort()
numbers.pop()
print(f"操作后: {numbers}")

# 遍历
for i, num in enumerate(numbers):
    print(f"  [{i}] = {num}", end="")
print()

# 列表推导式
squares = [x**2 for x in numbers if x % 2 == 0]
print(f"偶数的平方: {squares}")

# ============================================
# 2. 字符串（str）
# ============================================
print("\n" + "=" * 50)
print("2. 字符串")
print("=" * 50)

text = "  Hello, Python World!  "
print(f"原始: '{text}'")
print(f"去除空格: '{text.strip()}'")
print(f"分割: {text.split()}")
print(f"替换: {text.replace('Python', 'Java')}")

# 方法链
result = text.strip().lower().replace("world", "python")
print(f"方法链: '{result}'")

# 判断
print(f"是否字母: {'hello'.isalpha()}")
print(f"是否数字: {'123'.isdigit()}")

# ============================================
# 3. 元组（tuple）
# ============================================
print("\n" + "=" * 50)
print("3. 元组")
print("=" * 50)

# 创建
point = (10, 20)
rgb = (255, 128, 0)
print(f"点: {point}")
print(f"颜色: {rgb}")

# 解包
x, y = point
r, g, b = rgb
print(f"x={x}, y={y}")
print(f"R={r}, G={g}, B={b}")

# 函数返回元组
def min_max(lst):
    return min(lst), max(lst)

minimum, maximum = min_max([3, 1, 4, 1, 5, 9])
print(f"最小值: {minimum}, 最大值: {maximum}")

# 命名元组
from collections import namedtuple
Student = namedtuple("Student", ["name", "age", "grade"])
s = Student("Alice", 20, "A")
print(f"学生: {s.name}, {s.age}岁, {s.grade}")

# ============================================
# 4. 集合（set）
# ============================================
print("\n" + "=" * 50)
print("4. 集合")
print("=" * 50)

# 创建与去重
numbers = [1, 2, 2, 3, 3, 3, 4, 5, 5]
unique = set(numbers)
print(f"去重前: {numbers}")
print(f"去重后: {unique}")

# 集合运算
a = {1, 2, 3, 4, 5}
b = {4, 5, 6, 7, 8}
print(f"A: {a}")
print(f"B: {b}")
print(f"并集: {a | b}")
print(f"交集: {a & b}")
print(f"差集(A-B): {a - b}")
print(f"对称差: {a ^ b}")

# 成员检查（快速）
print(f"3 in A: {3 in a}")

# ============================================
# 5. 字典（dict）
# ============================================
print("\n" + "=" * 50)
print("5. 字典")
print("=" * 50)

# 创建
person = {
    "name": "Alice",
    "age": 25,
    "city": "Beijing",
    "skills": ["Python", "Java", "SQL"]
}
print(f"人员信息: {person}")

# 访问
print(f"姓名: {person['name']}")
print(f"年龄: {person.get('age')}")
print(f"国家: {person.get('country', '未知')}")

# 遍历
for key, value in person.items():
    if isinstance(value, list):
        print(f"  {key}: {', '.join(value)}")
    else:
        print(f"  {key}: {value}")

# 字典推导式
squares = {x: x**2 for x in range(5)}
print(f"平方表: {squares}")

# 合并
d1 = {"a": 1, "b": 2}
d2 = {"c": 3, "d": 4}
merged = {**d1, **d2}
print(f"合并: {merged}")

# ============================================
# 综合应用
# ============================================
print("\n" + "=" * 50)
print("综合应用 - 学生信息管理系统")
print("=" * 50)

students = [
    {"name": "Alice", "scores": {"Math": 95, "Physics": 88, "CS": 92}},
    {"name": "Bob", "scores": {"Math": 78, "Physics": 82, "CS": 91}},
    {"name": "Charlie", "scores": {"Math": 92, "Physics": 85, "CS": 96}},
]

# 计算平均分
for student in students:
    scores = list(student["scores"].values())
    avg = sum(scores) / len(scores)
    student["average"] = round(avg, 1)

# 按平均分排序
ranked = sorted(students, key=lambda s: s["average"], reverse=True)
print("成绩排名:")
for i, s in enumerate(ranked, 1):
    print(f"  {i}. {s['name']}: {s['average']}")

# 各科统计
subjects = {"Math", "Physics", "CS"}
for subject in sorted(subjects):
    scores = [s["scores"][subject] for s in students]
    print(f"\n{subject}:")
    print(f"  平均分: {sum(scores)/len(scores):.1f}")
    print(f"  最高分: {max(scores)}")
    print(f"  最低分: {min(scores)}")

# 优秀学生名单
excellent = {s["name"] for s in students if all(v >= 90 for v in s["scores"].values())}
print(f"\n全科优秀学生: {excellent if excellent else '无'}")

print("\n" + "=" * 50)
print("第三章 完")
print("=" * 50)
```

---

## 知识点速查表

| 容器 | 可变 | 有序 | 可重复 | 创建方式 | 关键方法 |
|------|------|------|--------|----------|----------|
| list | 是 | 是 | 是 | `[]` | `append`, `pop`, `sort` |
| str | 否 | 是 | - | `''` | `split`, `join`, `replace` |
| tuple | 否 | 是 | 是 | `()` | `count`, `index` |
| set | 是 | 否 | 否 | `{}` | `add`, `remove`, `update` |
| dict | 是 | 是(3.7+) | - | `{}` | `get`, `keys`, `items` |
| range | 否 | 是 | - | `range()` | 索引、切片、`len` |
| frozenset | 否 | 否 | 否 | `frozenset()` | `|`, `&`, `-`, `^` |
| bytes | 否 | 是 | - | `b"..."`, `bytes()` | `decode`, `hex`, `fromhex` |
| bytearray | 是 | 是 | - | `bytearray()` | `append`, `insert`, `pop` |

## 容器选择指南

| 需求 | 推荐容器 |
|------|----------|
| 需要索引访问 | 列表 |
| 需要不可变序列 | 元组 |
| 需要快速查找 | 集合 / 字典 |
| 需要去重 | 集合 |
| 需要键值映射 | 字典 |
| 文本处理 | 字符串 |
| 栈 / 队列 | 列表 |
| 数字序列循环 | range |
| 不可变集合 / 字典键 | frozenset |
| 二进制数据处理 | bytes / bytearray |
