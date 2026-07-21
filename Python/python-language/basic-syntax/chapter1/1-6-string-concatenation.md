# 字符串拼接

字符串拼接是将多个字符串合并成一个字符串的操作。

## 使用 + 运算符

```python
# 基本拼接
first = "Hello"
second = "World"
result = first + " " + second
print(result)  # Hello World

# 多个字符串拼接
greeting = "Good" + " " + "Morning" + " " + "Everyone"
print(greeting)  # Good Morning Everyone
```

### 注意事项

```python
# 不能拼接字符串和其他类型
age = 25
# message = "Age: " + age  # TypeError

# 需要先转换类型
message = "Age: " + str(age)
print(message)  # Age: 25
```

## 使用 += 运算符

```python
# 累加拼接
text = ""
text += "Hello"
text += " "
text += "World"
print(text)  # Hello World

# 实际应用
result = ""
for i in range(5):
    result += str(i) + " "
print(result)  # 0 1 2 3 4
```

## 使用 join() 方法

### 基本用法

```python
# 语法: separator.join(iterable)
words = ["Hello", "World", "Python"]
result = " ".join(words)
print(result)  # Hello World Python

# 不同分隔符
print("-".join(words))  # Hello-World-Python
print("".join(words))   # HelloWorldPython
print(", ".join(words)) # Hello, World, Python
```

### 性能优势

```python
# join() 比 + 更高效（大量拼接时）
import time

# 使用 + 拼接
start = time.time()
result = ""
for i in range(10000):
    result += str(i)
print(f"+ 耗时: {time.time() - start:.4f}秒")

# 使用 join() 拼接
start = time.time()
result = "".join(str(i) for i in range(10000))
print(f"join 耗时: {time.time() - start:.4f}秒")
```

## 使用 f-string

```python
# f-string 拼接
first = "Hello"
second = "World"
result = f"{first} {second}"
print(result)  # Hello World

# 表达式
name = "Alice"
age = 25
intro = f"我叫{name}，今年{age}岁"
print(intro)  # 我叫Alice，今年25岁
```

## 使用 format() 方法

```python
# 基本用法
result = "{} {}".format("Hello", "World")
print(result)  # Hello World

# 带索引
result = "{0} {1} {0}".format("Hello", "World")
print(result)  # Hello World Hello

# 带关键字
result = "{greeting} {name}".format(greeting="Hello", name="World")
print(result)  # Hello World
```

## 使用 % 运算符

```python
# 旧式格式化
name = "Alice"
age = 25
result = "我叫%s，今年%d岁" % (name, age)
print(result)  # 我叫Alice，今年25岁
```

## 字符串重复

```python
# 使用 * 运算符
separator = "-" * 20
print(separator)  # --------------------

# 重复字符串
echo = "Ha" * 3
print(echo)  # HaHaHa

# 创建分隔线
line = "=" * 50
print(line)
```

## 多行字符串拼接

### 使用反斜杠续行

```python
message = "这是第一行" \
          "这是第二行" \
          "这是第三行"
print(message)
```

### 使用括号

```python
message = (
    "这是第一行"
    "这是第二行"
    "这是第三行"
)
print(message)
```

### 使用三引号

```python
message = """这是第一行
这是第二行
这是第三行"""
print(message)
```

## 实际应用示例

### 构建文件路径

```python
import os

# 使用 os.path.join()
path = os.path.join("folder", "subfolder", "file.txt")
print(path)  # folder/subfolder/file.txt

# 手动拼接（不推荐）
path = "folder" + "/" + "subfolder" + "/" + "file.txt"
```

### 构建 URL

```python
base_url = "https://api.example.com"
endpoint = "/users"
user_id = "123"

url = base_url + endpoint + "/" + user_id
print(url)  # https://api.example.com/users/123

# 使用 f-string
url = f"{base_url}{endpoint}/{user_id}"
```

### 构建 SQL 查询

```python
table = "users"
columns = "name, age, email"
condition = "age > 18"

query = f"SELECT {columns} FROM {table} WHERE {condition}"
print(query)  # SELECT name, age, email FROM users WHERE age > 18
```

### 构建 HTML

```python
title = "我的网页"
content = "欢迎访问"

html = f"""
<html>
<head><title>{title}</title></head>
<body>
    <h1>{content}</h1>
</body>
</html>
"""
print(html)
```

## 性能比较

```python
import timeit

# 测试不同方法的性能
def test_plus():
    result = ""
    for i in range(1000):
        result += str(i)
    return result

def test_join():
    return "".join(str(i) for i in range(1000))

def test_format():
    return "".format(*(str(i) for i in range(1000)))

# 性能比较
print("+:     ", timeit.timeit(test_plus, number=100))
print("join:  ", timeit.timeit(test_join, number=100))
print("format:", timeit.timeit(test_format, number=100))
```
