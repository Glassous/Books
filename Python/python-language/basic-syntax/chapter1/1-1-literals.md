# 字面量

字面量（Literal）是直接在代码中表示固定值的数据。Python 中的字面量包括数值、字符串、布尔值和特殊值。

## 数值字面量

### 整数（int）

```python
# 十进制
decimal_num = 42

# 二进制（0b 或 0B 前缀）
binary_num = 0b1010  # 10

# 八进制（0o 或 0O 前缀）
octal_num = 0o52  # 42

# 十六进制（0x 或 0X 前缀）
hex_num = 0x2A  # 42

# 大数字可用下划线分隔提高可读性
large_num = 1_000_000
```

### 浮点数（float）

```python
# 标准小数形式
pi = 3.14159

# 科学计数法
light_speed = 3e8  # 300000000.0
avogadro = 6.022e23

# 下划线分隔
price = 19_999.99
```

### 复数（complex）

```python
# 使用 j 或 J 表示虚部
z1 = 3 + 4j
z2 = complex(3, 4)
```

## 字符串字面量

### 单引号和双引号

```python
name = 'Alice'
greeting = "Hello, World!"
```

### 三引号（多行字符串）

```python
paragraph = """这是
一个多行
字符串"""

doc = '''也可以
使用单引号
的三引号'''
```

### 转义字符

```python
# 常用转义字符
newline = "第一行\n第二行"
tab = "列1\t列2"
backslash = "C:\\Users\\path"
quote = "他说：\"你好\""

# 原始字符串（忽略转义）
raw = r"C:\Users\new_folder"
```

### f-string（格式化字符串）

```python
name = "Bob"
age = 25
intro = f"我叫{name}，今年{age}岁"
calc = f"2 + 3 = {2 + 3}"
```

## 布尔字面量

```python
is_active = True
is_deleted = False

# 布尔值在条件判断中使用
if is_active:
    print("账户已激活")
```

## 空值字面量

```python
# None 表示空值或不存在
result = None

# 检查是否为 None
if result is None:
    print("没有结果")
```

## 特殊字面量

### 字节字面量

```python
# bytes 类型
data = b"hello"
binary = b'\x00\x01\x02'
```

### 省略号字面量

```python
# Ellipsis，常用于类型提示和切片
def func(args, **kwargs): ...

# NumPy 中的多维切片
# arr[..., 0]
```

## 字面量的不可变性

Python 中的字面量（数字、字符串、元组等）是不可变的：

```python
s = "hello"
# s[0] = "H"  # TypeError: 'str' object does not support item assignment

nums = (1, 2, 3)
# nums[0] = 10  # TypeError: 'tuple' object does not support item assignment
```

## 字面量与类型转换

```python
# 整数转字符串
str(42)  # "42"

# 字符串转整数
int("42")  # 42

# 字符串转浮点数
float("3.14")  # 3.14

# 布尔转换
bool(0)  # False
bool("")  # False
bool(None)  # False
bool(1)  # True
```
