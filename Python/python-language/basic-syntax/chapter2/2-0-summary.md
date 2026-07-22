# 第二章 汇总

本章汇总了流程控制的核心知识点，包含速览、示例代码和完整示例文件。

---

## 速览

### 2.1 if 基础
- 条件判断：`if condition:`
- 真假值：`False`, `None`, `0`, `""`, `[]` 为假，其余为真
- 缩进：4 个空格定义代码块
- 三元运算符：`x if cond else y`

### 2.2 if else
- 双分支：`if-else`
- 多分支：`if-elif-else`
- 条件按顺序判断，匹配后跳过剩余分支

### 2.3 match
- 模式匹配（Python 3.10+）
- 支持字面量、元组、列表、字典、对象匹配
- 守卫条件：`case x if condition:`
- 通配符：`case _:`

### 2.4 while 循环
- 条件循环：`while condition:`
- `break`：退出循环
- `continue`：跳过当前迭代
- `else`：循环正常结束（未 break）时执行

### 2.5 for 循环
- 遍历可迭代对象
- `range()`：生成数字序列
- `enumerate()`：获取索引和值
- 列表推导式：`[x for x in iterable]`

### 2.6 嵌套循环
- 外层每执行一次，内层完整执行一轮
- `break` 只跳出当前最内层循环
- 使用标志变量跳出多层循环

---

## 示例代码

### 条件判断

```python
# if-elif-else
score = 85
if score >= 90:
    grade = "优秀"
elif score >= 80:
    grade = "良好"
elif score >= 70:
    grade = "中等"
elif score >= 60:
    grade = "及格"
else:
    grade = "不及格"
print(f"等级: {grade}")

# 三元运算符
age = 20
status = "成年人" if age >= 18 else "未成年人"
print(status)
```

### match 模式匹配

```python
def process(data):
    match data:
        case 1 | 2 | 3:
            return "小数字"
        case int(n) if n > 100:
            return "大数字"
        case str(s):
            return f"字符串: {s}"
        case _:
            return "其他"

print(process(2))      # 小数字
print(process(200))    # 大数字
print(process("hi"))   # 字符串: hi
```

### 循环

```python
# for 循环
for i in range(5):
    print(i, end=" ")
print()

# while 循环
count = 0
while count < 5:
    print(count, end=" ")
    count += 1
print()

# 嵌套循环
for i in range(3):
    for j in range(3):
        print(f"({i},{j})", end=" ")
    print()
```

### 循环控制

```python
# break
for i in range(10):
    if i == 5:
        break
    print(i, end=" ")  # 0 1 2 3 4
print()

# continue
for i in range(10):
    if i % 2 == 0:
        continue
    print(i, end=" ")  # 1 3 5 7 9
print()

# else
for i in range(3):
    print(i)
else:
    print("循环正常结束")
```

---

## 完整示例文件

```python
"""
第二章 流程控制 - 综合示例
包含：if、if-else、match、while、for、嵌套循环
"""

# ============================================
# 1. if 基础
# ============================================
print("=" * 50)
print("1. if 基础")
print("=" * 50)

x = 10
if x > 0:
    print(f"{x} 是正数")

# 真假值判断
items = []
if items:
    print("列表不为空")
else:
    print("列表为空")

# 三元运算符
result = "正数" if x > 0 else "非正数"
print(f"三元运算符: {result}")

# ============================================
# 2. if else
# ============================================
print("\n" + "=" * 50)
print("2. if else")
print("=" * 50)

def get_grade(score):
    if score >= 90:
        return "优秀"
    elif score >= 80:
        return "良好"
    elif score >= 70:
        return "中等"
    elif score >= 60:
        return "及格"
    else:
        return "不及格"

for score in [95, 82, 75, 68, 55]:
    print(f"分数 {score}: {get_grade(score)}")

# ============================================
# 3. match
# ============================================
print("\n" + "=" * 50)
print("3. match (Python 3.10+)")
print("=" * 50)

def describe_value(value):
    match value:
        case int(n) if n > 0:
            return f"正整数: {n}"
        case int(n):
            return f"非正整数: {n}"
        case str(s):
            return f"字符串: {s}"
        case [a, b, c]:
            return f"三元素列表: {a}, {b}, {c}"
        case _:
            return f"其他: {type(value).__name__}"

print(describe_value(42))
print(describe_value("hello"))
print(describe_value([1, 2, 3]))

# ============================================
# 4. while 循环
# ============================================
print("\n" + "=" * 50)
print("4. while 循环")
print("=" * 50)

# 计数器循环
i = 1
while i <= 5:
    print(i, end=" ")
    i += 1
print()

# 猜数字 (简化版)
import random
secret = random.randint(1, 10)
attempts = 0
found = False

while attempts < 3 and not found:
    attempts += 1
    guess = random.randint(1, 10)
    print(f"第 {attempts} 次猜: {guess}")
    if guess == secret:
        print(f"猜对了！数字是 {secret}")
        found = True

if not found:
    print(f"没猜中！数字是 {secret}")

# ============================================
# 5. for 循环
# ============================================
print("\n" + "=" * 50)
print("5. for 循环")
print("=" * 50)

# 遍历列表
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit, end=" ")
print()

# 使用 range
for i in range(1, 6):
    print(f"2 x {i} = {2 * i}")

# 使用 enumerate
for i, fruit in enumerate(fruits, 1):
    print(f"{i}. {fruit}")

# 列表推导式
squares = [x ** 2 for x in range(10) if x % 2 == 0]
print(f"偶数的平方: {squares}")

# ============================================
# 6. 嵌套循环
# ============================================
print("\n" + "=" * 50)
print("6. 嵌套循环")
print("=" * 50)

# 乘法表
print("九九乘法表:")
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f"{j}x{i}={i*j}", end="\t")
    print()

# 打印矩形
print("\n5x5 矩形:")
for i in range(5):
    for j in range(5):
        print("*", end=" ")
    print()

# 二维列表
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print("\n矩阵转置:")
transposed = [[matrix[j][i] for j in range(len(matrix))] for i in range(len(matrix[0]))]
for row in transposed:
    print(row)

# ============================================
# 综合应用
# ============================================
print("\n" + "=" * 50)
print("综合应用")
print("=" * 50)

# 用户登录验证
def login_system():
    correct_user = "admin"
    correct_pass = "123456"
    max_attempts = 3

    for attempt in range(1, max_attempts + 1):
        print(f"\n第 {attempt} 次登录尝试")
        username = input("用户名: ")
        password = input("密码: ")

        if not username:
            print("用户名不能为空")
            continue
        if not password:
            print("密码不能为空")
            continue
        if username != correct_user:
            print("用户名不存在")
            continue
        if password != correct_pass:
            print("密码错误")
            continue
        print("登录成功！")
        return True
    else:
        print("登录失败，已达最大尝试次数")
        return False

# login_system()  # 取消注释运行

# 冒泡排序
def bubble_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        swapped = False
        for j in range(n - 1 - i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr

numbers = [64, 34, 25, 12, 22, 11, 90]
print(f"\n冒泡排序:")
print(f"排序前: {numbers}")
print(f"排序后: {bubble_sort(numbers)}")

# 统计字符
def count_chars(text):
    vowels = "aeiou"
    consonants = "bcdfghjklmnpqrstvwxyz"
    result = {"vowels": 0, "consonants": 0, "digits": 0, "spaces": 0}

    for char in text.lower():
        if char in vowels:
            result["vowels"] += 1
        elif char in consonants:
            result["consonants"] += 1
        elif char.isdigit():
            result["digits"] += 1
        elif char == " ":
            result["spaces"] += 1

    return result

text = "Hello Python 3! Welcome to 2024."
stats = count_chars(text)
print(f"\n字符统计结果:")
for key, value in stats.items():
    print(f"  {key}: {value}")

print("\n" + "=" * 50)
print("第二章 完")
print("=" * 50)
```

---

## 知识点速查表

| 类别 | 内容 | 示例 |
|------|------|------|
| if 基础 | 条件判断、缩进、三元 | `if x > 0:` |
| if else | 双分支、多分支 | `if-elif-else` |
| match | 模式匹配、守卫 | `match x: case 1:` |
| while | 条件循环、计数器 | `while x < 10:` |
| for | 遍历、range、enumerate | `for i in range(10):` |
| break | 退出循环 | `break` |
| continue | 跳过当前迭代 | `continue` |
| else | 循环正常结束执行 | `for x in y: else:` |
| 嵌套 | 多层循环、break 作用域 | `for i in: for j in:` |
