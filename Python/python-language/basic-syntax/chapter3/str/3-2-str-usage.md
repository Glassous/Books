# 字符串用法详解

## 查找与判断

```python
s = "Hello, Python World!"

# find() - 查找子串索引
print(s.find("Python"))     # 7
print(s.find("Java"))       # -1

# index() - 类似 find，找不到则报错
print(s.index("Python"))    # 7

# rfind() - 从右查找
print(s.rfind("o"))         # 15

# startswith() / endswith()
print(s.startswith("Hello"))   # True
print(s.endswith("!"))         # True

# count() - 统计次数
print(s.count("o"))            # 3
```

## 大小写转换

```python
text = "Hello, World!"

print(text.upper())          # HELLO, WORLD!
print(text.lower())          # hello, world!
print(text.title())          # Hello, World!
print(text.capitalize())     # Hello, world!
print(text.swapcase())       # hELLO, wORLD!

# 判断
print("ABC".isupper())       # True
print("abc".islower())       # True
print("Hello".istitle())     # True
```

## 格式化与对齐

```python
text = "Python"

# 对齐
print(text.center(20))       #       Python
print(text.ljust(20))        # Python
print(text.rjust(20))        #               Python
print(text.zfill(10))        # 0000Python

# 去除空白
text2 = "  hello  "
print(text2.strip())         # hello
print(text2.lstrip())        # hello
print(text2.rstrip())        #   hello

# 去除指定字符
url = "www.example.com"
print(url.strip("w.com"))    # example
```

## 分割与连接

```python
# split() - 分割
s = "apple,banana,cherry"
print(s.split(","))          # ['apple', 'banana', 'cherry']

# rsplit() - 从右分割
print(s.rsplit(",", 1))      # ['apple,banana', 'cherry']

# splitlines() - 按行分割
lines = "a\nb\nc"
print(lines.splitlines())    # ['a', 'b', 'c']

# partition() - 分割为三部分
print(s.partition(","))      # ('apple', ',', 'banana,cherry')

# join() - 连接
words = ["Hello", "World", "Python"]
print(" ".join(words))       # Hello World Python
print("-".join(words))       # Hello-World-Python
print("".join(words))        # HelloWorldPython
```

## 替换与翻译

```python
# replace() - 替换
s = "I like Python, Python is great"
print(s.replace("Python", "Java"))
print(s.replace("Python", "Java", 1))  # 只替换1次

# translate() - 字符映射翻译
table = str.maketrans("aeiou", "12345")
print("hello world".translate(table))  # h2ll4 w4rld

# 删除字符
table = str.maketrans("", "", "aeiou")
print("hello world".translate(table))  # hll wrld
```

## 字符类型判断

```python
# 字母数字判断
print("abc123".isalnum())    # True
print("abc".isalpha())       # True
print("123".isdigit())       # True
print("  ".isspace())        # True
print("123".isdecimal())     # True
print("123".isnumeric())     # True

# 其他判断
print("Hello".isprintable())  # True
print("Hello".isascii())      # True
```

## 前缀后缀处理

```python
filename = "document.txt"

# 检查前缀后缀
print(filename.startswith("doc"))     # True
print(filename.endswith(".txt"))      # True

# 移除前缀后缀
print(filename.removeprefix("doc"))   # ument.txt
print(filename.removesuffix(".txt"))  # document

# 应用：文件路径处理
files = ["readme.txt", "image.png", "readme.md", "script.py"]
text_files = [f for f in files if f.endswith(".txt")]
print(text_files)  # ['readme.txt']
```

## 字符串切片高级用法

```python
s = "Python Programming"

# 基本切片
print(s[0:6])     # Python
print(s[7:])      # Programming

# 步长
print(s[::2])     # Pto rgamn
print(s[::-1])    # gnimmargorP nohtyP

# 负数索引切片
print(s[-11:])    # Programming
print(s[-11:-4])  # Program

# 切片赋值（字符串不可变，但可以通过切片创建新字符串）
words = s.split()
first = words[0]
last = words[1]
```

## 字符串迭代与处理

```python
# 逐字符处理
text = "Hello"
for char in text:
    print(char)

# 使用 enumerate
for i, char in enumerate(text):
    print(f"{i}: {char}")

# 过滤字符
digits = "".join(c for c in "abc123def456" if c.isdigit())
print(digits)  # 123456
```
