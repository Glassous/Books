# 第四章 汇总

本章汇总了函数的核心知识点，包含速览、示例代码和完整示例文件。

---

## 速览

### 4.1 函数定义
- `def` 关键字定义函数：`def func():`
- 函数体使用缩进
- `return` 返回值，无 return 返回 `None`
- `pass` 作为空函数占位符

### 4.2 参数与返回值
- 必需参数（位置参数）
- 关键字参数（`name=value`）
- 混合使用（位置在前，关键字在后）
- 类型注解：`def add(a: int, b: int) -> int`

### 4.3 函数说明文档
- 文档字符串（docstring）位于函数体第一行
- 单行：`"""简述功能"""`
- 多行：参数、返回值、示例说明
- 访问方式：`func.__doc__`、`help(func)`

### 4.4 函数嵌套调用
- 一个函数中调用另一个函数
- 返回值直接作为参数传递（链式调用）
- 内部定义辅助函数

### 4.5 变量作用域
- LEGB 规则：Local → Enclosing → Global → Built-in
- `global` 修改全局变量
- `nonlocal` 修改外部函数变量
- 避免覆盖内置函数名

### 4.6 传参方式
- 位置参数：按顺序传递
- 关键字参数：按名称传递
- 仅限位置参数：使用 `/`
- 仅限关键字参数：使用 `*`

### 4.7 默认参数
- `def func(a, b=10):`
- 默认参数在定义时求值
- **陷阱**：避免使用可变对象作为默认值
- 推荐使用 `None` 替代可变默认值

### 4.8 不定长参数
- `*args`：收集多余位置参数（元组）
- `**kwargs`：收集多余关键字参数（字典）
- `*` 和 `**` 解包序列和字典

### 4.9 函数类型
- 函数是一等公民，可赋值、传参、返回
- 高阶函数：`map()`、`filter()`、`sorted(key=)`
- 闭包：函数记住其创建时的环境

### 4.10 匿名函数
- `lambda 参数: 表达式`
- 适用于简单操作
- 常与 `sorted()`、`map()`、`filter()` 配合

### 4.11 函数类型注解
- 语法：`def func(a: int) -> str:`
- 容器注解：`List[int]`、`Dict[str, int]`
- `Optional`：可选类型（`Optional[str] = None`）
- `Union`：联合类型（`Union[int, str]`）
- `Callable`：函数作为参数类型
- 类型别名：为复杂类型定义简短名称
- 注解不影响运行，仅用于提示

### 4.12 案例
- 递归：函数调用自身，需有递归出口
- 阶乘：`n! = n × (n-1)!`
- 斐波那契：`F(n) = F(n-1) + F(n-2)`
- 汉诺塔：递归移动盘子问题

### 4.13 模块
- 导入方式：`import`、`from ... import`、别名
- `if __name__ == '__main__'`：区分模块与脚本
- 自定义模块：创建 `.py` 文件即可
- 包：包含 `__init__.py` 的目录
- 子包：嵌套的包目录结构
- 标准库：`math`、`random`、`os`、`sys`、`json` 等

---

## 示例代码

### 函数定义与参数

```python
# 函数定义
def greet(name, greeting="Hello"):
    """向指定用户问好"""
    return f"{greeting}, {name}!"

# 不同传参方式
print(greet("Alice"))                    # 位置参数
print(greet("Bob", greeting="Hi"))       # 关键字参数
print(greet("Charlie", "Hey"))           # 位置参数

# 不定长参数
def sum_all(*args):
    return sum(args)

def print_info(**kwargs):
    for k, v in kwargs.items():
        print(f"  {k}: {v}")

print(sum_all(1, 2, 3, 4, 5))
print_info(name="Alice", age=25)
```

### 作用域

```python
x = 100  # 全局变量

def outer():
    x = 10  # 闭包变量

    def inner():
        x = 1  # 局部变量
        print(f"局部: {x}")

    inner()
    print(f"闭包: {x}")

outer()
print(f"全局: {x}")
```

### lambda 与高阶函数

```python
numbers = [1, 2, 3, 4, 5, 6]

# map
squared = list(map(lambda x: x ** 2, numbers))

# filter
evens = list(filter(lambda x: x % 2 == 0, numbers))

# sorted
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 92},
    {"name": "Charlie", "grade": 78}
]
sorted_students = sorted(students, key=lambda s: s["grade"])

print(f"平方: {squared}")
print(f"偶数: {evens}")
print(f"按成绩排序: {sorted_students}")
```

### 递归

```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

def fibonacci(n):
    """使用循环实现的斐波那契"""
    if n <= 0:
        return 0
    if n == 1:
        return 1
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b

def hanoi(n, source, target, aux):
    if n == 1:
        print(f"移动盘子 1: {source} -> {target}")
        return
    hanoi(n - 1, source, aux, target)
    print(f"移动盘子 {n}: {source} -> {target}")
    hanoi(n - 1, aux, target, source)

print(f"5! = {factorial(5)}")
print(f"F(10) = {fibonacci(10)}")
print("\n3 层汉诺塔:")
hanoi(3, "A", "C", "B")
```

---

## 完整示例文件

```python
"""
第四章 函数 - 综合示例
包含：函数定义、参数、作用域、lambda、类型注解、递归、阶乘、斐波那契、汉诺塔、模块
"""

# ============================================
# 1. 函数基础
# ============================================
print("=" * 50)
print("1. 函数基础")
print("=" * 50)

def add(a: int, b: int) -> int:
    """两数相加"""
    return a + b

def multiply(a: int, b: int = 2) -> int:
    """乘法，默认乘 2"""
    return a * b

print(f"add(3, 5) = {add(3, 5)}")
print(f"multiply(5) = {multiply(5)}")
print(f"multiply(5, 3) = {multiply(5, 3)}")

# ============================================
# 2. 参数传递方式
# ============================================
print("\n" + "=" * 50)
print("2. 参数传递方式")
print("=" * 50)

def example(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
    print(f"pos1={pos1}, pos2={pos2}")
    print(f"pos_or_kwd={pos_or_kwd}")
    print(f"kwd1={kwd1}, kwd2={kwd2}")

example(1, 2, 3, kwd1=4, kwd2=5)

# ============================================
# 3. 不定长参数
# ============================================
print("\n" + "=" * 50)
print("3. 不定长参数")
print("=" * 50)

def flexible_func(name, *args, **kwargs):
    print(f"名称: {name}")
    print(f"额外位置参数: {args}")
    print(f"额外关键字参数: {kwargs}")

flexible_func("test", 1, 2, 3, color="red", size=10)

# ============================================
# 4. 作用域演示
# ============================================
print("\n" + "=" * 50)
print("4. 作用域")
print("=" * 50)

x = "全局变量"

def outer():
    x = "外层变量"

    def inner():
        nonlocal x
        x = "修改外层"
        print(f"inner 中: {x}")

    inner()
    print(f"outer 中: {x}")

outer()
print(f"全局: {x}")

# ============================================
# 5. 高阶函数与 lambda
# ============================================
print("\n" + "=" * 50)
print("5. 高阶函数与 lambda")
print("=" * 50)

numbers = [4, 7, 2, 9, 1, 5]

# 排序
sorted_nums = sorted(numbers)
sorted_desc = sorted(numbers, reverse=True)
sorted_by_mod = sorted(numbers, key=lambda x: x % 3)

print(f"升序: {sorted_nums}")
print(f"降序: {sorted_desc}")
print(f"按模3排序: {sorted_by_mod}")

# 闭包
def make_power(n):
    def power(x):
        return x ** n
    return power

square = make_power(2)
cube = make_power(3)
print(f"3² = {square(3)}")
print(f"2³ = {cube(2)}")

# ============================================
# 6. 递归与经典案例
# ============================================
print("\n" + "=" * 50)
print("6. 递归与经典案例")
print("=" * 50)

def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

def fibonacci(n):
    if n <= 0:
        return 0
    if n == 1:
        return 1
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b

print("阶乘:")
for i in range(0, 11):
    print(f"  {i}! = {factorial(i)}")

print("\n斐波那契数列:")
for i in range(10):
    print(f"  F({i}) = {fibonacci(i)}")

print("\n汉诺塔（3 个盘子）:")
def hanoi(n, src, tgt, aux):
    if n == 1:
        print(f"  {src} -> {tgt}")
    else:
        hanoi(n - 1, src, aux, tgt)
        print(f"  {src} -> {tgt}")
        hanoi(n - 1, aux, tgt, src)

hanoi(3, "A", "C", "B")

# ============================================
# 综合应用：学生成绩管理系统
# ============================================
print("\n" + "=" * 50)
print("7. 综合应用：学生成绩管理")
print("=" * 50)

def calculate_grade(score):
    """根据分数计算等级"""
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

def process_scores(scores):
    """处理成绩列表"""
    return list(map(calculate_grade, scores))

def analyze_scores(scores):
    """分析成绩统计信息"""
    return {
        "平均分": sum(scores) / len(scores),
        "最高分": max(scores),
        "最低分": min(scores),
        "及格率": len([s for s in scores if s >= 60]) / len(scores) * 100
    }

scores = [85, 92, 73, 58, 90, 67, 88, 76]
grades = process_scores(scores)
stats = analyze_scores(scores)

for score, grade in zip(scores, grades):
    print(f"  {score}分 -> {grade}")

print(f"\n统计信息:")
for key, value in stats.items():
    print(f"  {key}: {value if key != '及格率' else f'{value:.1f}%'}")

# 使用 lambda 排序
ranked = sorted(
    [{"name": f"学生{i+1}", "score": s} for i, s in enumerate(scores)],
    key=lambda x: x["score"],
    reverse=True
)

print("\n排名:")
for i, student in enumerate(ranked, 1):
    print(f"  第{i}名: {student['name']} ({student['score']}分)")

print("\n" + "=" * 50)
print("第四章 完")
print("=" * 50)
```

---

## 知识点速查表

| 类别 | 内容 | 示例 |
|------|------|------|
| 函数定义 | def、return、pass | `def f(): return x` |
| 参数 | 位置/关键字/混合 | `f(a, b=1)` |
| 文档字符串 | 函数说明 | `"""说明文字"""` |
| 嵌套调用 | 函数内调用函数 | `f(g(x))` |
| 作用域 | LEGB 规则 | `global`, `nonlocal` |
| 传参方式 | 仅位置/仅关键字 | `def f(a, /, *, b):` |
| 默认参数 | 默认值、可变陷阱 | `def f(a=[]):` |
| 不定长参数 | *args, **kwargs | `def f(*args, **kwargs)` |
| 函数类型 | 一等公民、高阶函数 | `map(f, lst)` |
| 匿名函数 | lambda 表达式 | `lambda x: x**2` |
| 类型注解 | 参数/返回值类型提示 | `def f(x: int) -> str:` |
| 递归 | 函数自调用 | `def f(): f()` |
| 阶乘 | n! | `n * f(n-1)` |
| 斐波那契 | 数列生成 | `F(n) = F(n-1) + F(n-2)` |
| 汉诺塔 | 三柱移动 | 递归移动 n-1 个盘子 |
| 模块 | 导入/自定义模块/包 | `import math; from math import pi` |
