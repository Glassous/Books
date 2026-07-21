# 字符串定义

字符串是 Python 中最常用的数据类型之一，用于表示文本数据。

## 字符串的创建

### 使用引号

```python
# 单引号
name = 'Alice'
message = 'Hello, World!'

# 双引号
greeting = "Hello, Python!"
quote = "He said, 'hi'"

# 混合引号
text1 = "It's a dog"
text2 = 'He said "hello"'
```

### 三引号（多行字符串）

```python
# 三双引号
paragraph = """这是第一行
这是第二行
这是第三行"""

# 三单引号
doc = '''多行字符串
可以包含换行符
很方便'''
```

### 原始字符串

```python
# 原始字符串（r-string）忽略转义字符
path = r"C:\Users\new_folder"
regex = r"\d+\.\d+"

# 普通字符串需要转义
path2 = "C:\\Users\\new_folder"
```

### 字节字符串

```python
# 字节字符串
data = b"hello"
binary = b'\x00\x01\x02'
```

## 转义字符

### 常用转义字符

```python
# 换行符
print("第一行\n第二行")

# 制表符
print("列1\t列2\t列3")

# 反斜杠
print("C:\\Users\\path")

# 引号
print("他说：\"你好\"")
print('It\'s a dog')
```

### 转义字符列表

| 转义字符 | 描述 |
|----------|------|
| `\n` | 换行 |
| `\t` | 制表符 |
| `\\` | 反斜杠 |
| `\'` | 单引号 |
| `\"` | 双引号 |
| `\r` | 回车 |
| `\b` | 退格 |
| `\f` | 换页 |
| `\0` | 空字符 |
| `\ooo` | 八进制值 |
| `\xhh` | 十六进制值 |
| `\uxxxx` | Unicode 字符 |

## 字符串索引

### 正向索引

```python
text = "Python"
#   索引: 0  1  2  3  4  5
#   字符: P  y  t  h  o  n

print(text[0])   # P
print(text[1])   # y
print(text[5])   # n
```

### 反向索引

```python
text = "Python"
#   索引: -6 -5 -4 -3 -2 -1
#   字符:  P  y  t  h  o  n

print(text[-1])  # n
print(text[-6])  # P
```

## 字符串切片

### 基本切片

```python
text = "Hello, Python!"

# 语法: text[start:end:step]
print(text[0:5])    # Hello
print(text[7:13])   # Python
print(text[:5])     # Hello（从开头开始）
print(text[7:])     # Python!（到结尾）
```

### 带步长的切片

```python
text = "Hello, Python!"

# 步长为2
print(text[::2])    # Hlo yhn

# 反转字符串
print(text[::-1])   # !nohtyP ,olleH

# 负步长
print(text[13:6:-1]) # nohtyP
```

## 字符串长度

```python
text = "Hello, Python!"
length = len(text)
print(length)  # 14

# 空字符串
empty = ""
print(len(empty))  # 0
```

## 字符串不可变性

```python
text = "Hello"
# text[0] = "h"  # TypeError: 'str' object does not support item assignment

# 创建新字符串
new_text = "h" + text[1:]
print(new_text)  # hello
```

## 特殊字符串

### 空字符串

```python
empty1 = ""
empty2 = ''
empty3 = str()
```

### 包含空格的字符串

```python
space = " "
spaces = "   "
```

### Unicode 字符串

```python
# Unicode 字符
chinese = "你好"
emoji = "😊"
special = "©®™"
```

## 字符串编码

### 编码和解码

```python
# 编码为字节
text = "你好"
bytes_data = text.encode("utf-8")
print(bytes_data)  # b'\xe4\xbd\xa0\xe5\xa5\xbd'

# 解码为字符串
decoded = bytes_data.decode("utf-8")
print(decoded)  # 你好
```

### 查看编码

```python
import sys
print(sys.getdefaultencoding())  # utf-8
```

## 多行字符串

### 使用三引号

```python
html = """
<html>
<head>
    <title>标题</title>
</head>
<body>
    <p>内容</p>
</body>
</html>
"""
```

### 使用反斜杠续行

```python
message = "这是一个" \
          "很长的" \
          "字符串"
```

### 使用括号

```python
message = (
    "这是一个"
    "很长的"
    "字符串"
)
```
