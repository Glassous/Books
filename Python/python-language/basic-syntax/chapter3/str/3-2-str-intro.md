# 字符串（str）介绍

字符串是 Python 中用于表示文本数据的序列类型，由 Unicode 字符组成。

## 什么是字符串

字符串是**有序**、**不可变**的字符序列，用引号括起来表示。

```python
# 单引号
s1 = 'hello'

# 双引号
s2 = "world"

# 三引号（多行）
s3 = """多行
字符串"""
```

## 字符串的特点

### 不可变性
字符串一旦创建就不能修改：

```python
s = "hello"
# s[0] = "H"  # TypeError

# 修改需要创建新字符串
s = "H" + s[1:]  # "Hello"
```

### 有序性
字符串维护字符的顺序，支持索引和切片：

```python
s = "Python"
print(s[0])    # P
print(s[-1])   # n
print(s[0:3])  # Pyt
```

### Unicode 支持
Python 3 字符串基于 Unicode，支持多种语言：

```python
print("你好")        # 中文
print("Hello")       # 英文
print("こんにちは")  # 日文
print("😊")         # Emoji
```

## 字符串的编码

```python
# UTF-8 编码
text = "你好"
encoded = text.encode("utf-8")
print(encoded)  # b'\xe4\xbd\xa0\xe5\xa5\xbd'
print(encoded.decode("utf-8"))  # 你好
```

## 字符串 vs 字节串

```python
# 字符串
text = "hello"

# 字节串
data = b"hello"

# 转换
text = data.decode("utf-8")
data = text.encode("utf-8")
```

## 字符串长度

```python
s = "hello"
print(len(s))  # 5

japanese = "こんにちは"
print(len(japanese))  # 5

emoji = "😊"
print(len(emoji))  # 1

# 空字符串
empty = ""
print(len(empty))  # 0
```

## 创建字符串

```python
# 直接创建
s1 = "hello"

# str() 构造函数
s2 = str(42)        # "42"
s3 = str(3.14)      # "3.14"
s4 = str([1, 2])    # "[1, 2]"

# 字符串拼接创建
s5 = "a" + "b" + "c"  # "abc"

# 重复创建
s6 = "ha" * 3  # "hahaha"
```

## 字符串的存储

```python
# 每个字符是 Unicode 码点
s = "Python"
for char in s:
    print(f"{char}: {ord(char)}")

# P: 80
# y: 121
# t: 116
# h: 104
# o: 111
# n: 110
```
