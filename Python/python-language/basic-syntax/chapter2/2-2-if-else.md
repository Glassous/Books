# if else

`if else` 语句用于在两个分支中选择一个执行。

## if-else 语句

```python
# 基本语法
if condition:
    statement_block_1
else:
    statement_block_2
```

### 基本示例

```python
age = 15

if age >= 18:
    print("成年人")
else:
    print("未成年人")
```

### 真假值判断

```python
name = ""

if name:
    print(f"你好, {name}")
else:
    print("名字不能为空")
```

## if-elif-else 语句

### 基本语法

```python
if condition1:
    statement_block_1
elif condition2:
    statement_block_2
elif condition3:
    statement_block_3
else:
    statement_block_else
```

### 成绩等级

```python
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

print(f"成绩: {score}, 等级: {grade}")
```

## elif 的使用技巧

### 多个条件判断

```python
def get_weekday(day_num):
    if day_num == 1:
        return "星期一"
    elif day_num == 2:
        return "星期二"
    elif day_num == 3:
        return "星期三"
    elif day_num == 4:
        return "星期四"
    elif day_num == 5:
        return "星期五"
    elif day_num == 6:
        return "星期六"
    elif day_num == 7:
        return "星期日"
    else:
        return "无效的日期"

print(get_weekday(3))  # 星期三
```

### 按顺序判断

```python
def get_ticket_price(age):
    if age < 0:
        return "无效年龄"
    elif age < 6:
        return "免费"
    elif age < 18:
        return "半价"
    elif age < 60:
        return "全价"
    else:
        return "免费"

print(get_ticket_price(25))  # 全价
print(get_ticket_price(5))   # 免费
```

## if-else 嵌套

```python
x = 10
y = 20

if x > 0:
    if y > 0:
        print("第一象限")
    else:
        print("第四象限")
else:
    if y > 0:
        print("第二象限")
    else:
        print("第三象限")
```

## 多条件判断

### 使用 and

```python
age = 25
has_license = True

if age >= 18 and has_license:
    print("可以开车")
else:
    print("不能开车")
```

### 使用 or

```python
is_student = True
is_senior = False

if is_student or is_senior:
    print("享受折扣")
else:
    print("全价")
```

### 使用 not

```python
is_raining = False

if not is_raining:
    print("适合出行")
else:
    print("带伞出门")
```

## 条件表达式优化

### 使用字典替代多个 elif

```python
# 使用字典映射
def get_weekday_dict(day_num):
    weekdays = {
        1: "星期一",
        2: "星期二",
        3: "星期三",
        4: "星期四",
        5: "星期五",
        6: "星期六",
        7: "星期日"
    }
    return weekdays.get(day_num, "无效的日期")

print(get_weekday_dict(3))  # 星期三
```

### 使用列表判断

```python
# 多个值判断
vowel = "a"
if vowel in ["a", "e", "i", "o", "u"]:
    print("元音")
else:
    print("辅音")
```

## 实际应用

### 计算器

```python
def calculator(a, operator, b):
    if operator == "+":
        return a + b
    elif operator == "-":
        return a - b
    elif operator == "*":
        return a * b
    elif operator == "/":
        if b == 0:
            return "除数不能为零"
        return a / b
    elif operator == "//":
        return a // b
    elif operator == "%":
        return a % b
    elif operator == "**":
        return a ** b
    else:
        return "无效运算符"

print(calculator(10, "+", 3))   # 13
print(calculator(10, "/", 3))   # 3.333...
```

### 登录系统

```python
def login_system(username, password):
    users = {
        "admin": "123456",
        "user": "password"
    }

    if not username:
        return "用户名不能为空"
    elif not password:
        return "密码不能为空"
    elif username not in users:
        return "用户名不存在"
    elif users[username] != password:
        return "密码错误"
    else:
        return "登录成功"

print(login_system("admin", "123456"))  # 登录成功
print(login_system("admin", "wrong"))   # 密码错误
```

### BMI 计算

```python
def bmi_category(weight, height):
    bmi = weight / (height ** 2)

    if bmi < 18.5:
        return "偏瘦"
    elif bmi < 24:
        return "正常"
    elif bmi < 28:
        return "偏胖"
    else:
        return "肥胖"

print(bmi_category(70, 1.75))   # 正常
```

## 常见错误

```python
# 错误：忘记冒号
# if x > 0  # SyntaxError

# 错误：缩进不一致
# if x > 0:
#     print("正数")
#   print("下一行")  # IndentationError

# 错误：空 if 块
# if x > 0:
#     pass  # 需要使用 pass 占位

# 正确
if x > 0:
    pass  # 稍后实现
```
