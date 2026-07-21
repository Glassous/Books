# 比较运算符

比较运算符用于比较两个值，返回布尔值 `True` 或 `False`。

## 基本比较运算符

### 等于（==）

```python
# 数值比较
print(10 == 10)   # True
print(10 == 20)   # False

# 字符串比较
print("hello" == "hello")  # True
print("hello" == "Hello")  # False（区分大小写）

# 不同类型比较
print(10 == 10.0)   # True（值相等）
print(0 == False)    # True
print("" == False)   # False
```

### 不等于（!=）

```python
print(10 != 20)    # True
print(10 != 10)    # False

print("hello" != "world")  # True
print("hello" != "hello")  # False
```

### 大于（>）

```python
print(10 > 5)     # True
print(5 > 10)     # False
print(10 > 10)    # False

# 字符串按字典序比较
print("b" > "a")  # True
print("abc" > "abd")  # False
```

### 小于（<）

```python
print(5 < 10)     # True
print(10 < 5)     # False
print(10 < 10)    # False

# 浮点数比较
print(3.14 < 3.15)  # True
```

### 大于等于（>=）

```python
print(10 >= 10)   # True
print(10 >= 5)    # True
print(5 >= 10)    # False
```

### 小于等于（<=）

```python
print(10 <= 10)   # True
print(5 <= 10)    # True
print(10 <= 5)    # False
```

## 链式比较

Python 支持链式比较运算符，使代码更简洁。

```python
# 链式比较
x = 5
print(1 < x < 10)      # True（等价于 1 < x and x < 10）
print(1 < x < 3)       # False

# 多个条件
print(1 < x < 10 < 100)  # True

# 等价形式
print(1 < x and x < 10)  # True
```

## 身份比较（is）

### is 与 == 的区别

```python
# == 比较值
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b)   # True（值相等）
print(a is b)   # False（不是同一个对象）

# is 比较内存地址
a = [1, 2, 3]
b = a
print(a is b)   # True（同一个对象）

# None 比较推荐使用 is
x = None
print(x is None)      # True
print(x == None)      # True（但不推荐）
```

### 小整数池

```python
# Python 缓存了小整数（-5 到 256）
a = 256
b = 256
print(a is b)   # True

a = 257
b = 257
print(a is b)   # False（可能，取决于实现）
```

## 成员比较（in）

```python
# 列表
fruits = ["apple", "banana", "cherry"]
print("apple" in fruits)    # True
print("grape" in fruits)    # False
print("grape" not in fruits)  # True

# 字符串
text = "Hello, World!"
print("World" in text)  # True
print("world" in text)  # False（区分大小写）

# 字典（检查键）
person = {"name": "Alice", "age": 25}
print("name" in person)   # True
print("Alice" in person)  # False（检查的是键，不是值）
```

## 比较不同类型

### 数值类型

```python
# int 和 float 可以比较
print(10 == 10.0)    # True
print(10 == 10.000000000000001)  # True（浮点数精度问题）

# int 和 bool
print(1 == True)     # True
print(0 == False)    # True
print(2 == True)     # False
```

### 序列比较

```python
# 字符串按字典序比较
print("abc" < "abd")   # True
print("abc" < "abcd")  # True（前缀关系）

# 列表按元素顺序比较
print([1, 2, 3] < [1, 2, 4])  # True
print([1, 2] < [1, 2, 3])     # True
```

## 浮点数比较注意事项

```python
# 浮点数精度问题
print(0.1 + 0.2 == 0.3)  # False

# 正确的比较方法
import math
print(math.isclose(0.1 + 0.2, 0.3))  # True

# 自定义精度
def float_equal(a, b, rel_tol=1e-9, abs_tol=0.0):
    return abs(a - b) <= max(rel_tol * max(abs(a), abs(b)), abs_tol)

print(float_equal(0.1 + 0.2, 0.3))  # True
```

## 运算符优先级

比较运算符的优先级（从高到低）：
1. `is`, `is not`
2. `in`, `not in`
3. `<`, `<=`, `>`, `>=`, `!=`, `==`

```python
# 优先级示例
x = 5
print(1 < x < 10 and x != 3)  # True
# 等价于
print((1 < x < 10) and (x != 3))  # True
```

## 实际应用

### 成绩等级判断

```python
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

print(get_grade(85))  # 良好
```

### 输入验证

```python
def validate_age(age):
    if not isinstance(age, int):
        return "年龄必须是整数"
    if age < 0 or age > 150:
        return "年龄必须在0-150之间"
    return "有效"

print(validate_age(25))    # 有效
print(validate_age(-5))    # 年龄必须在0-150之间
print(validate_age(3.5))   # 年龄必须是整数
```

### 范围检查

```python
def is_valid_password(password):
    has_length = len(password) >= 8
    has_upper = any(c.isupper() for c in password)
    has_lower = any(c.islower() for c in password)
    has_digit = any(c.isdigit() for c in password)
    
    return all([has_length, has_upper, has_lower, has_digit])

print(is_valid_password("Abc12345"))   # True
print(is_valid_password("abc12345"))   # False（没有大写字母）
```

### 排序比较

```python
# 自定义排序
students = [
    {"name": "Alice", "score": 85},
    {"name": "Bob", "score": 92},
    {"name": "Charlie", "score": 78}
]

# 按成绩排序
sorted_students = sorted(students, key=lambda x: x["score"], reverse=True)
for student in sorted_students:
    print(f"{student['name']}: {student['score']}")
```

## 常见错误

```python
# 错误：使用 = 而不是 ==
# if x = 5:  # SyntaxError

# 错误：比较 None 使用 ==
# if x == None:  # 不推荐

# 正确
if x is None:
    pass
```
