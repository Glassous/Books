# 第一章 汇总

本章汇总了 Python 基础语法的核心知识点，包含速览、示例代码和完整示例文件。

---

## 速览

### 1.1 字面量
- **数值**：整数 `42`、浮点数 `3.14`、复数 `3+4j`
- **字符串**：`"hello"`、`'world'`、`"""多行"""`
- **布尔**：`True`、`False`
- **空值**：`None`

### 1.2 变量
- 动态类型：变量无需声明类型
- 赋值创建：`x = 10`
- 引用模型：变量是对象的引用

### 1.3 标识符
- 命名规则：字母/下划线开头，可含数字
- 命名风格：`snake_case`（变量）、`CamelCase`（类）、`UPPER_CASE`（常量）
- 避免关键字：`if`、`for`、`class` 等

### 1.4 数据类型
- 数值：`int`、`float`、`complex`
- 序列：`list`、`tuple`、`range`、`str`
- 映射：`dict`
- 集合：`set`、`frozenset`
- 布尔：`bool`（`int` 的子类）

### 1.5 字符串定义
- 引号：单引号、双引号、三引号
- 原始字符串：`r"path\to\file"`
- 转义字符：`\n`、`\t`、`\\`
- 索引和切片：`text[0]`、`text[1:5]`

### 1.6 字符串拼接
- `+` 运算符：`"Hello" + " World"`
- `join()` 方法：`" ".join(["Hello", "World"])`
- `*` 重复：`"Ha" * 3`

### 1.7 字符串格式化
- f-string：`f"{name} is {age}"`
- format()：`"{} is {}".format(name, age)`
- % 运算符：`"%s is %d" % (name, age)`

### 1.8 输入与输出
- 输出：`print(value, sep, end)`
- 输入：`input(prompt)`（返回字符串）
- 文件：`open()`、`read()`、`write()`

### 1.9 算术运算符
- 基本：`+`、`-`、`*`、`/`
- 整除：`//`
- 取模：`%`
- 幂运算：`**`

### 1.10 赋值运算符
- 基本：`=`
- 增强：`+=`、`-=`、`*=`、`/=`、`//=`、`%=`、`**=`
- 海象运算符：`:=`（Python 3.8+）

### 1.11 比较运算符
- 比较：`==`、`!=`、`>`、`<`、`>=`、`<=`
- 身份：`is`、`is not`
- 成员：`in`、`not in`

### 1.12 逻辑运算符
- 与：`and`（短路求值）
- 或：`or`（短路求值）
- 非：`not`

### 1.13 位运算符
- 按位与 `&`、按位或 `|`、按位异或 `^`、按位取反 `~`
- 左移 `<<`、右移 `>>`
- 应用：权限控制、奇偶判断、变量交换

---

## 示例代码

### 字面量与变量

```python
# 各种字面量
integer_num = 42
float_num = 3.14
text = "Hello, Python!"
is_active = True
nothing = None

# 变量赋值
name = "Alice"
age = 25
x, y, z = 1, 2, 3

print(f"名字: {name}, 年龄: {age}")
```

### 字符串操作

```python
# 字符串定义
s1 = "单引号"
s2 = "双引号"
s3 = """多行
字符串"""

# 拼接
greeting = "Hello" + " " + "World"
words = ["Python", "is", "awesome"]
sentence = " ".join(words)

# 格式化
name = "Bob"
age = 30
print(f"{name} is {age} years old")
print("{} is {} years old".format(name, age))
```

### 运算符

```python
# 算术运算符
print(10 + 3)   # 13
print(10 - 3)   # 7
print(10 * 3)   # 30
print(10 / 3)   # 3.333...
print(10 // 3)  # 3
print(10 % 3)   # 1
print(2 ** 3)   # 8

# 比较运算符
print(10 > 5)   # True
print(10 == 10) # True
print(10 != 5)  # True

# 逻辑运算符
x = 15
print(x > 10 and x < 20)  # True
print(x < 10 or x > 12)   # True
print(not x < 10)          # True
```

### 输入输出

```python
# 输出
print("Hello, World!")
print("A", "B", "C", sep="-")  # A-B-C
print("不换行", end=" ")
print("换行")

# 输入
name = input("请输入名字: ")
age = int(input("请输入年龄: "))
print(f"你好, {name}! 明年你 {age + 1} 岁")
```

---

## 完整示例文件

以下是一个包含本章所有知识点的综合示例：

```python
"""
第一章 基础语法 - 综合示例
包含：字面量、变量、标识符、数据类型、字符串、输入输出、运算符
"""

# ============================================
# 1. 字面量 (Literals)
# ============================================
print("=" * 50)
print("1. 字面量")
print("=" * 50)

# 整数字面量
decimal_num = 42          # 十进制
binary_num = 0b1010       # 二进制
octal_num = 0o52          # 八进制
hex_num = 0x2A            # 十六进制
large_num = 1_000_000     # 下划线分隔

# 浮点数
pi = 3.14159
light_speed = 3e8

# 复数
complex_num = 3 + 4j

# 字符串
single_quote = 'Hello'
double_quote = "World"
triple_quote = """多行
字符串"""
raw_string = r"C:\Users\path"

# 布尔值
is_true = True
is_false = False

# 空值
nothing = None

print(f"整数: {decimal_num}, {binary_num}, {octal_num}, {hex_num}")
print(f"浮点数: {pi}, {light_speed}")
print(f"复数: {complex_num}")
print(f"字符串: {single_quote}, {double_quote}")
print(f"布尔: {is_true}, {is_false}")
print(f"空值: {nothing}")

# ============================================
# 2. 变量 (Variables)
# ============================================
print("\n" + "=" * 50)
print("2. 变量")
print("=" * 50)

# 变量赋值
x = 10
name = "Alice"
is_valid = True

# 多变量赋值
a, b, c = 1, 2, 3
m = n = p = 0

# 交换变量
a, b = 10, 20
a, b = b, a
print(f"交换后: a={a}, b={b}")

# 动态类型
dynamic_var = 42
print(f"类型: {type(dynamic_var)}")
dynamic_var = "hello"
print(f"类型变为: {type(dynamic_var)}")

# ============================================
# 3. 标识符 (Identifiers)
# ============================================
print("\n" + "=" * 50)
print("3. 标识符")
print("=" * 50)

# 合法标识符
user_name = "Alice"
_private = 10
MAX_SIZE = 100

# 命名约定
# 变量/函数: snake_case
def calculate_total():
    pass

# 类: CamelCase
class UserAccount:
    pass

# 常量: UPPER_CASE
PI = 3.14159

print(f"变量: {user_name}, {_private}, {MAX_SIZE}")

# ============================================
# 4. 数据类型 (Data Types)
# ============================================
print("\n" + "=" * 50)
print("4. 数据类型")
print("=" * 50)

# 数值类型
int_val = 42
float_val = 3.14
complex_val = 3 + 4j

# 序列类型
list_val = [1, 2, 3, 4, 5]
tuple_val = (1, 2, 3)
range_val = range(5)

# 映射类型
dict_val = {"name": "Alice", "age": 25}

# 集合类型
set_val = {1, 2, 3, 3, 4}
frozenset_val = frozenset([1, 2, 3])

# 布尔类型
bool_val = True

print(f"int: {int_val}, type: {type(int_val)}")
print(f"float: {float_val}, type: {type(float_val)}")
print(f"list: {list_val}, type: {type(list_val)}")
print(f"dict: {dict_val}, type: {type(dict_val)}")
print(f"set: {set_val}, type: {type(set_val)}")

# ============================================
# 5. 字符串定义 (String Definition)
# ============================================
print("\n" + "=" * 50)
print("5. 字符串定义")
print("=" * 50)

# 字符串创建
s1 = "Hello"
s2 = 'World'
s3 = """多行
字符串"""

# 转义字符
escaped = "第一行\n第二行\t制表符"
print(escaped)

# 原始字符串
raw = r"C:\Users\new_folder"
print(f"原始字符串: {raw}")

# 字符串索引
text = "Python"
print(f"第一个字符: {text[0]}")
print(f"最后一个字符: {text[-1]}")

# 字符串切片
print(f"切片: {text[0:3]}")
print(f"反转: {text[::-1]}")

# ============================================
# 6. 字符串拼接 (String Concatenation)
# ============================================
print("\n" + "=" * 50)
print("6. 字符串拼接")
print("=" * 50)

# + 运算符
greeting = "Hello" + " " + "World"
print(f"+ 拼接: {greeting}")

# join() 方法
words = ["Python", "is", "awesome"]
sentence = " ".join(words)
print(f"join: {sentence}")

# 重复
ha = "Ha" * 3
print(f"重复: {ha}")

# f-string 拼接
name = "Alice"
age = 25
intro = f"我叫{name}，今年{age}岁"
print(f"f-string: {intro}")

# ============================================
# 7. 字符串格式化 (String Formatting)
# ============================================
print("\n" + "=" * 50)
print("7. 字符串格式化")
print("=" * 50)

pi = 3.14159

# f-string 格式化
print(f"保留两位小数: {pi:.2f}")
print(f"百分比: {0.85:.1%}")
print(f"千位分隔: {1000000:,}")

# format() 方法
print("{}".format("Hello"))
print("{0} {1}".format("Hello", "World"))

# % 运算符
print("圆周率: %.2f" % pi)

# ============================================
# 8. 输入与输出 (Input/Output)
# ============================================
print("\n" + "=" * 50)
print("8. 输入与输出")
print("=" * 50)

# print() 函数
print("默认输出")
print("A", "B", "C", sep="-")
print("不换行", end=" ")
print("换行")

# 演示 input()（注释掉避免阻塞）
# name = input("请输入名字: ")
# age = int(input("请输入年龄: "))
# print(f"你好, {name}!")

print("(input() 已跳过，避免阻塞)")

# ============================================
# 9. 算术运算符 (Arithmetic Operators)
# ============================================
print("\n" + "=" * 50)
print("9. 算术运算符")
print("=" * 50)

a, b = 10, 3

print(f"{a} + {b} = {a + b}")     # 加法
print(f"{a} - {b} = {a - b}")     # 减法
print(f"{a} * {b} = {a * b}")     # 乘法
print(f"{a} / {b} = {a / b:.2f}") # 除法
print(f"{a} // {b} = {a // b}")   # 整除
print(f"{a} % {b} = {a % b}")     # 取模
print(f"{a} ** {b} = {a ** b}")   # 幂运算

# ============================================
# 10. 赋值运算符 (Assignment Operators)
# ============================================
print("\n" + "=" * 50)
print("10. 赋值运算符")
print("=" * 50)

x = 10
print(f"初始值: {x}")

x += 5
print(f"x += 5: {x}")

x -= 3
print(f"x -= 3: {x}")

x *= 2
print(f"x *= 2: {x}")

x //= 3
print(f"x //= 3: {x}")

x **= 2
print(f"x **= 2: {x}")

# ============================================
# 11. 比较运算符 (Comparison Operators)
# ============================================
print("\n" + "=" * 50)
print("11. 比较运算符")
print("=" * 50)

a, b = 10, 20

print(f"{a} == {b}: {a == b}")   # 等于
print(f"{a} != {b}: {a != b}")   # 不等于
print(f"{a} > {b}: {a > b}")     # 大于
print(f"{a} < {b}: {a < b}")     # 小于
print(f"{a} >= {b}: {a >= b}")   # 大于等于
print(f"{a} <= {b}: {a <= b}")   # 小于等于

# 链式比较
x = 15
print(f"10 < {x} < 20: {10 < x < 20}")

# 身份比较
a = [1, 2, 3]
b = [1, 2, 3]
c = a
print(f"a == b: {a == b}")
print(f"a is b: {a is b}")
print(f"a is c: {a is c}")

# 成员比较
fruits = ["apple", "banana", "cherry"]
print(f"'apple' in fruits: {'apple' in fruits}")

# ============================================
# 12. 逻辑运算符 (Logical Operators)
# ============================================
print("\n" + "=" * 50)
print("12. 逻辑运算符")
print("=" * 50)

x, y = True, False

print(f"True and False: {x and y}")   # 与
print(f"True or False: {x or y}")     # 或
print(f"not True: {not x}")           # 非

# 短路求值
print(f"10 > 5 and 3 < 5: {10 > 5 and 3 < 5}")
print(f"10 > 5 or 3 > 5: {10 > 5 or 3 > 5}")

# 实际应用
age = 25
income = 50000
if age >= 18 and income >= 30000:
    print("符合贷款条件")

# 默认值设置
name = "" or "Anonymous"
print(f"默认值: {name}")

# ============================================
# 综合应用示例
# ============================================
print("\n" + "=" * 50)
print("综合应用示例")
print("=" * 50)

# 温度转换
def celsius_to_fahrenheit(celsius):
    return celsius * 9/5 + 32

def fahrenheit_to_celsius(fahrenheit):
    return (fahrenheit - 32) * 5/9

c = 25
f = celsius_to_fahrenheit(c)
print(f"{c}°C = {f}°F")

# 成绩等级判断
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

scores = [95, 82, 75, 68, 55]
for score in scores:
    print(f"分数 {score}: {get_grade(score)}")

# 字符串处理
text = "Hello, Python World!"
print(f"大写: {text.upper()}")
print(f"小写: {text.lower()}")
print(f"单词数: {len(text.split())}")

# 列表操作
numbers = [3, 1, 4, 1, 5, 9, 2, 6]
print(f"排序前: {numbers}")
print(f"排序后: {sorted(numbers)}")
print(f"最大值: {max(numbers)}")
print(f"最小值: {min(numbers)}")
print(f"总和: {sum(numbers)}")

print("\n" + "=" * 50)
print("第一章 完")
print("=" * 50)
```

---

## 知识点速查表

| 类别 | 内容 | 示例 |
|------|------|------|
| 字面量 | 整数、浮点数、字符串、布尔、None | `42`, `3.14`, `"hello"`, `True`, `None` |
| 变量 | 赋值、多变量赋值、交换 | `x = 10`, `a, b = 1, 2` |
| 标识符 | 命名规则、命名约定 | `user_name`, `CamelCase`, `MAX_SIZE` |
| 数据类型 | int, float, str, list, dict, set | `type(x)` |
| 字符串 | 引号、转义、切片 | `"hello"`, `text[0:5]` |
| 拼接 | +、join、* | `"a" + "b"`, `" ".join(list)` |
| 格式化 | f-string、format、% | `f"{x}"`, `"{}".format(x)` |
| 输入输出 | print、input | `print()`, `input()` |
| 算术 | +, -, *, /, //, %, ** | `10 // 3` |
| 赋值 | =, +=, -=, *= | `x += 5` |
| 比较 | ==, !=, >, <, >=, <= | `x > 10` |
| 逻辑 | and, or, not | `x > 5 and x < 10` |
| 位运算 | &, |, ^, ~, <<, >> | `x & 1`, `x << 2` |
