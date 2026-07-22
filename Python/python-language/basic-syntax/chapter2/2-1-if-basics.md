# if 基础

`if` 语句用于根据条件执行代码，是 Python 中最基本的分支控制结构。

## 基本语法

```python
if condition:
    statement
```

## 基本 if 语句

```python
# 基本条件判断
age = 18

if age >= 18:
    print("成年人")
```

### 条件为真时执行

```python
# 各种条件表达式
x = 10

if x > 0:
    print("正数")

if x % 2 == 0:
    print("偶数")

if True:
    print("总是执行")
```

## 缩进规则

Python 使用缩进定义代码块，通常为 4 个空格：

```python
if True:
    print("缩进 4 个空格")
    print("同一个代码块")
    if True:
        print("嵌套代码块需要更多缩进")
print("不在 if 块中")
```

## 条件表达式

### 使用比较运算符

```python
score = 85

if score >= 60:
    print("及格")

if score >= 90:
    print("优秀")
```

### 使用逻辑运算符

```python
age = 25
income = 50000

if age >= 18 and income >= 30000:
    print("符合贷款条件")

if age < 18 or age > 65:
    print("特殊人群")
```

### 使用成员运算符

```python
fruits = ["apple", "banana", "cherry"]

if "apple" in fruits:
    print("有苹果")

if "grape" not in fruits:
    print("没有葡萄")
```

### 使用身份运算符

```python
x = None

if x is None:
    print("x 是空值")

if x is not None:
    print("x 有值")
```

## 真假值判断

Python 中的值可以直接用于条件判断：

### 假值（Falsy）
```python
# 以下值在条件判断中为 False
if False: pass
if None: pass
if 0: pass
if 0.0: pass
if "": pass
if []: pass
if {}: pass
if (): pass
if set(): pass
```

### 真值（Truthy）
```python
# 以下值在条件判断中为 True
if True: pass
if 1: pass
if -1: pass
if "hello": pass
if [1, 2]: pass
if {"key": "value"}: pass
if (1,): pass
```

### 实际应用

```python
# 检查列表是否为空
items = []
if items:
    print("列表不为空")
else:
    print("列表为空")

# 检查字符串是否非空
name = "Alice"
if name:
    print(f"名字是 {name}")

# 检查值是否存在
value = None
if value:
    print("有值")
else:
    print("无值")
```

## 嵌套 if

```python
x = 10
y = 20

if x > 0:
    print("x 是正数")
    if y > 0:
        print("y 也是正数")
        if x + y > 25:
            print("x + y 大于 25")
```

## 单行 if

```python
# 单行 if（不推荐复杂表达式）
x = 10
if x > 0: print("正数")

# 使用逗号分隔多个语句
if x > 0: print("正数"); print("非零")
```

## 条件表达式（三元运算符）

```python
# 语法：value_if_true if condition else value_if_false
x = 10
result = "正数" if x > 0 else "非正数"
print(result)  # 正数

# 嵌套条件表达式
score = 85
grade = "优秀" if score >= 90 else "良好" if score >= 80 else "中等"
print(grade)  # 良好
```

## 实际应用

### 年龄验证

```python
def check_age(age):
    if age < 0:
        return "无效年龄"
    if age < 18:
        return "未成年人"
    if age < 60:
        return "成年人"
    return "老年人"

print(check_age(25))   # 成年人
print(check_age(15))   # 未成年人
print(check_age(65))   # 老年人
```

### 登录验证

```python
def login(username, password):
    if not username:
        print("用户名不能为空")
        return False
    if not password:
        print("密码不能为空")
        return False
    if len(password) < 6:
        print("密码长度不足")
        return False
    print("登录成功")
    return True

login("admin", "123456")
```

### 数值判断

```python
def classify_number(n):
    if n == 0:
        return "零"
    if n > 0:
        if n % 2 == 0:
            return "正偶数"
        else:
            return "正奇数"
    else:
        if n % 2 == 0:
            return "负偶数"
        else:
            return "负奇数"

print(classify_number(10))   # 正偶数
print(classify_number(-7))   # 负奇数
```
