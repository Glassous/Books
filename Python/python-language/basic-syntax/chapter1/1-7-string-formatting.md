# 字符串格式化

Python 提供了多种字符串格式化方法，用于将变量插入字符串中。

## f-string（推荐）

f-string 是 Python 3.6+ 引入的格式化方法，使用 `f` 前缀和 `{}` 占位符。

### 基本用法

```python
name = "Alice"
age = 25

# 基本格式化
message = f"我叫{name}，今年{age}岁"
print(message)  # 我叫Alice，今年25岁

# 表达式
x = 10
y = 20
result = f"{x} + {y} = {x + y}"
print(result)  # 10 + 20 = 30
```

### 格式规范

```python
# 数字格式化
pi = 3.14159

# 保留小数位数
print(f"圆周率: {pi:.2f}")  # 圆周率: 3.14

# 宽度和对齐
print(f"右对齐: {42:>10}")  # 右对齐:         42
print(f"左对齐: {42:<10}")  # 左对齐: 42        
print(f"居中: {42:^10}")    # 居中:     42    

# 填充字符
print(f"填充: {42:0>10}")   # 填充: 0000000042
print(f"填充: {42:*<10}")   # 填充: 42********

# 千位分隔符
print(f"数字: {1000000:,}")  # 数字: 1,000,000
print(f"数字: {1000000:_}")  # 数字: 1_000_000
```

### 数字格式化类型

```python
num = 42

# 不同进制
print(f"十进制: {num:d}")    # 十进制: 42
print(f"二进制: {num:b}")    # 二进制: 101010
print(f"八进制: {num:o}")    # 八进制: 52
print(f"十六进制: {num:x}")  # 十六进制: 2a
print(f"十六进制: {num:X}")  # 十六进制: 2A

# 浮点数
print(f"科学计数法: {pi:e}")  # 科学计数法: 3.141590e+00
print(f"百分比: {0.85:.1%}") # 百分比: 85.0%
```

### 表达式和函数调用

```python
# 表达式
print(f"结果: {2 * 3 + 1}")  # 结果: 7

# 函数调用
name = "alice"
print(f"大写: {name.upper()}")  # 大写: ALICE

# 列表推导
numbers = [1, 2, 3, 4, 5]
print(f"平方: {[x**2 for x in numbers]}")  # 平方: [1, 4, 9, 16, 25]
```

## format() 方法

### 基本用法

```python
# 位置参数
print("{} {}".format("Hello", "World"))  # Hello World

# 索引参数
print("{0} {1} {0}".format("Hello", "World"))  # Hello World Hello

# 关键字参数
print("{name} is {age} years old".format(name="Alice", age=25))
```

### 格式规范

```python
# 数字格式化
print("{:.2f}".format(3.14159))  # 3.14

# 宽度和对齐
print("{:>10}".format(42))      #         42
print("{:<10}".format(42))      # 42        
print("{:^10}".format(42))      #     42    

# 填充
print("{:0>10}".format(42))     # 0000000042
print("{:*<10}".format(42))     # 42********

# 千位分隔符
print("{:,}".format(1000000))   # 1,000,000
```

### 访问属性和索引

```python
# 访问对象属性
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

person = Person("Alice", 25)
print("{0.name} is {0.age}".format(person))

# 访问列表索引
data = [10, 20, 30]
print("{0[0]} {0[2]}".format(data))  # 10 30
```

## % 运算符（旧式）

### 基本用法

```python
# 字符串
name = "Alice"
print("Hello, %s!" % name)  # Hello, Alice!

# 整数
age = 25
print("Age: %d" % age)  # Age: 25

# 浮点数
pi = 3.14159
print("Pi: %.2f" % pi)  # Pi: 3.14

# 多个值
print("%s is %d years old" % ("Alice", 25))
```

### 格式化符号

| 符号 | 描述 |
|------|------|
| `%s` | 字符串 |
| `%d` | 整数 |
| `%f` | 浮点数 |
| `%e` | 科学计数法 |
| `%x` | 十六进制 |
| `%o` | 八进制 |
| `%%` | 字面量 % |

```python
# 示例
print("%%s: %s" % "hello")      # %s: hello
print("十进制: %d" % 42)         # 十进制: 42
print("十六进制: %x" % 255)      # 十六进制: ff
print("科学计数法: %e" % 1000)   # 科学计数法: 1.000000e+03
```

## 字符串对齐

```python
text = "Python"

# 左对齐
print(f"|{text:<20}|")  # |Python              |

# 右对齐
print(f"|{text:>20}|")  # |              Python|

# 居中
print(f"|{text:^20}|")  # |       Python       |

# 填充字符
print(f"|{text:*^20}|")  # |*******Python*******|
```

## 数字格式化

```python
# 整数补零
print(f"{42:05d}")  # 00042

# 浮点数精度
print(f"{3.14159:.2f}")  # 3.14
print(f"{3.14159:.4f}")  # 3.1416

# 科学计数法
print(f"{1000:.2e}")  # 1.00e+03

# 百分比
print(f"{0.856:.1%}")  # 85.6%

# 正负号
print(f"{42:+d}")   # +42
print(f"{-42:+d}")  # -42
```

## 实际应用

### 生成报告

```python
def generate_report(name, score, total):
    percentage = score / total * 100
    return f"""
    成绩报告
    --------
    姓名: {name}
    分数: {score}/{total}
    百分比: {percentage:.1f}%
    等级: {'优秀' if percentage >= 90 else '良好' if percentage >= 80 else '及格'}
    """

print(generate_report("Alice", 85, 100))
```

### 构建 URL

```python
def build_url(base, path, params=None):
    url = f"{base}/{path}"
    if params:
        query = "&".join(f"{k}={v}" for k, v in params.items())
        url += f"?{query}"
    return url

url = build_url(
    "https://api.example.com",
    "users",
    {"page": 1, "limit": 10}
)
print(url)  # https://api.example.com/users?page=1&limit=10
```

### 日志格式化

```python
import datetime

def log_message(level, message):
    timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    return f"[{timestamp}] {level:>8}: {message}"

print(log_message("INFO", "程序启动"))
print(log_message("ERROR", "文件未找到"))
```
