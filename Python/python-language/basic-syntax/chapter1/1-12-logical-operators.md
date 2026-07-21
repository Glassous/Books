# 逻辑运算符

逻辑运算符用于组合多个条件表达式，返回布尔值。

## 基本逻辑运算符

### and（与）

```python
# 两个条件都为 True 时返回 True
print(True and True)    # True
print(True and False)   # False
print(False and True)   # False
print(False and False)  # False

# 实际应用
age = 25
income = 50000
if age >= 18 and income >= 30000:
    print("符合贷款条件")
```

### or（或）

```python
# 至少一个条件为 True 时返回 True
print(True or True)    # True
print(True or False)   # True
print(False or True)   # True
print(False or False)  # False

# 实际应用
is_student = True
is_senior = False
if is_student or is_senior:
    print("享受折扣")
```

### not（非）

```python
# 取反
print(not True)   # False
print(not False)  # True

# 实际应用
is_raining = False
if not is_raining:
    print("天气晴朗")
```

## 短路求值

Python 使用短路求值，即在确定结果后不再计算剩余部分。

### and 短路

```python
# 如果第一个条件为 False，不计算第二个条件
def func():
    print("func 被调用")
    return True

# 不会调用 func()
result = False and func()
print(result)  # False

# 会调用 func()
result = True and func()
print(result)  # func 被调用 \n True
```

### or 短路

```python
# 如果第一个条件为 True，不计算第二个条件
def func():
    print("func 被调用")
    return True

# 不会调用 func()
result = True or func()
print(result)  # True

# 会调用 func()
result = False or func()
print(result)  # func 被调用 \n True
```

## 逻辑运算符的返回值

### and 返回最后一个真值或第一个假值

```python
# 返回实际值，不一定是布尔值
print(1 and 2)      # 2
print(0 and 2)      # 0
print(1 and 0)      # 0
print(0 and 0)      # 0

# 空值
print("" and "hello")  # ""
print("hello" and "")  # ""
print("hello" and "world")  # world
```

### or 返回第一个真值或最后一个假值

```python
print(1 or 2)      # 1
print(0 or 2)      # 2
print(1 or 0)      # 1
print(0 or 0)      # 0

# 空值
print("" or "hello")  # hello
print("hello" or "")  # hello
print("" or "")       # ""
```

## 组合使用

### 复杂条件

```python
# 多个条件组合
age = 25
income = 50000
has_property = True

if (age >= 18 and income >= 30000) or has_property:
    print("符合贷款条件")

# 使用括号提高可读性
if (age >= 18 and age <= 65) and (income >= 30000 or has_property):
    print("符合条件")
```

### 优先级

逻辑运算符优先级（从高到低）：
1. `not`
2. `and`
3. `or`

```python
# 优先级示例
print(True or False and False)   # True（先计算 and）
print((True or False) and False)  # False（括号改变优先级）

# 等价于
print(True or (False and False))  # True
```

## 实际应用

### 默认值设置

```python
# 使用 or 设置默认值
name = "" or "Anonymous"
print(name)  # Anonymous

name = "Alice" or "Anonymous"
print(name)  # Alice

# 使用 and 条件赋值
is_admin = True
admin_level = is_admin and "superadmin" or "user"
print(admin_level)  # superadmin
```

### 权限检查

```python
def check_permission(user_role, action):
    is_admin = user_role == "admin"
    is_owner = user_role == "owner"
    is_read_action = action == "read"
    
    # 管理员或所有者可以执行任何操作
    if is_admin or is_owner:
        return True
    
    # 普通用户只能读取
    if is_read_action:
        return True
    
    return False

print(check_permission("admin", "delete"))   # True
print(check_permission("user", "read"))      # True
print(check_permission("user", "delete"))    # False
```

### 输入验证

```python
def validate_input(data):
    errors = []
    
    if not data.get("name"):
        errors.append("姓名不能为空")
    
    if not data.get("email") or "@" not in data["email"]:
        errors.append("邮箱格式不正确")
    
    age = data.get("age")
    if not age or not isinstance(age, int) or age < 0 or age > 150:
        errors.append("年龄必须在0-150之间")
    
    return len(errors) == 0, errors

# 测试
data1 = {"name": "Alice", "email": "alice@example.com", "age": 25}
data2 = {"name": "", "email": "invalid", "age": -5}

print(validate_input(data1))  # (True, [])
print(validate_input(data2))  # (False, [...])
```

### 条件执行

```python
# 安全的属性访问
class User:
    def __init__(self, name, address=None):
        self.name = name
        self.address = address

user = User("Alice")

# 使用 and 避免 AttributeError
city = user.address and user.address.city
print(city)  # None（不会报错）

# 使用 or 提供默认值
city = (user.address and user.address.city) or "未知城市"
print(city)  # 未知城市
```

## 逻辑运算符的特殊用法

### 作为条件表达式

```python
# 使用 and/or 实现简单的条件赋值
x = 5
result = x > 0 and "正数" or "非正数"
print(result)  # 正数

# 注意：当结果为假值时可能出错
x = 0
result = x > 0 and "正数" or "非正数"
print(result)  # 非正数
```

### 过滤数据

```python
# 使用 and 过滤
numbers = [1, 0, 2, False, 3, None, 4]
filtered = [x for x in numbers if x and x > 0]
print(filtered)  # [1, 2, 3, 4]

# 使用 or 提供默认值
data = [None, 0, "", "hello", False, "world"]
with_values = [x or "default" for x in data]
print(with_values)  # ['default', 'default', 'default', 'hello', 'default', 'world']
```

## 注意事项

```python
# 避免过度复杂的条件
# 不推荐
if (a and b or c) and (d or not e) or (f and g):
    pass

# 推荐：提取为变量或函数
condition1 = a and b or c
condition2 = d or not e
condition3 = f and g
if condition1 and condition2 or condition3:
    pass

# 或者使用函数
def is_valid():
    return (a and b or c) and (d or not e) or (f and g)

if is_valid():
    pass
```

## 性能考虑

```python
# 将最可能为 False 的条件放在 and 前面
if expensive_check() and cheap_check():
    pass

# 将最可能为 True 的条件放在 or 前面
if cheap_check() or expensive_check():
    pass
```
