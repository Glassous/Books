# 数据类型

Python 是动态类型语言，变量不需要声明类型。Python 提供了多种内置数据类型。

## 数值类型

### 整数（int）

```python
# 整数
age = 25
count = -10
big_num = 1000000

# 不同进制
binary = 0b1010    # 二进制
octal = 0o52       # 八进制
hex_num = 0x2A     # 十六进制
```

### 浮点数（float）

```python
# 浮点数
pi = 3.14159
price = 99.99
temperature = -5.5

# 科学计数法
light_speed = 3e8
avogadro = 6.022e23
```

### 复数（complex）

```python
# 复数
z1 = 3 + 4j
z2 = complex(3, 4)

# 访问实部和虚部
print(z1.real)  # 3.0
print(z1.imag)  # 4.0
```

## 字符串类型（str）

```python
# 字符串
name = "Alice"
message = 'Hello, World!'
paragraph = """多行
字符串"""

# 字符串是不可变的
text = "hello"
# text[0] = "H"  # TypeError
```

## 布尔类型（bool）

```python
# 布尔值
is_active = True
is_deleted = False

# 布尔值是整数的子类
print(True + True)  # 2
print(True * 10)    # 10
```

## 空值类型（NoneType）

```python
# None 表示空值
result = None
data = None

# 检查 None
if result is None:
    print("没有结果")
```

## 序列类型

### 列表（list）

```python
# 列表 - 有序、可变
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", True, 3.14]

# 列表操作
fruits.append("orange")
fruits[0] = "grape"
```

### 元组（tuple）

```python
# 元组 - 有序、不可变
coordinates = (10, 20)
colors = ("red", "green", "blue")
single = (1,)  # 单元素元组需要逗号

# 元组解包
x, y = coordinates
```

### 范围（range）

```python
# range - 不可变的整数序列
numbers = range(5)        # 0, 1, 2, 3, 4
sequence = range(1, 10)   # 1, 2, ..., 9
step = range(0, 10, 2)    # 0, 2, 4, 6, 8
```

## 映射类型

### 字典（dict）

```python
# 字典 - 键值对、可变
person = {
    "name": "Alice",
    "age": 25,
    "city": "Beijing"
}

# 访问和修改
print(person["name"])
person["age"] = 26
person["email"] = "alice@example.com"
```

## 集合类型

### 集合（set）

```python
# 集合 - 无序、不重复
fruits = {"apple", "banana", "cherry"}
numbers = {1, 2, 3, 3, 4}  # 自动去重

# 集合操作
fruits.add("orange")
fruits.remove("apple")
```

### 冻结集合（frozenset）

```python
# 冻结集合 - 不可变的集合
frozen = frozenset([1, 2, 3])
```

## 二进制类型

### 字节（bytes）

```python
# 字节 - 不可变
data = b"hello"
binary = b'\x00\x01\x02'
```

### 字节数组（bytearray）

```python
# 字节数组 - 可变
arr = bytearray(b"hello")
arr[0] = 72  # 修改为 'H'
```

## 类型检查

### type() 函数

```python
x = 42
print(type(x))        # <class 'int'>
print(type("hello"))  # <class 'str'>
print(type([1, 2]))   # <class 'list'>
```

### isinstance() 函数

```python
# 检查类型
print(isinstance(42, int))        # True
print(isinstance("hello", str))   # True
print(isinstance(42, (int, str))) # True
```

## 类型转换

```python
# 数值转换
int("42")        # 字符串转整数
float("3.14")    # 字符串转浮点数
str(42)          # 整数转字符串

# 序列转换
list("hello")    # ['h', 'e', 'l', 'l', 'o']
tuple([1, 2, 3]) # (1, 2, 3)
set([1, 2, 2])   # {1, 2}

# 布尔转换
bool(0)          # False
bool("")         # False
bool(None)       # False
bool(1)          # True
```

## 可变与不可变类型

### 不可变类型
- int, float, complex
- str
- tuple
- frozenset
- bytes

### 可变类型
- list
- dict
- set
- bytearray

```python
# 不可变类型示例
x = 10
y = x
y = 20
print(x)  # 10，x 不变

# 可变类型示例
list1 = [1, 2, 3]
list2 = list1
list2.append(4)
print(list1)  # [1, 2, 3, 4]，list1 也被修改
```
