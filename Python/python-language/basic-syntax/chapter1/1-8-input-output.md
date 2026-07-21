# 输入与输出

Python 提供了简单易用的输入输出功能，用于与用户交互和显示结果。

## 输出：print() 函数

### 基本输出

```python
# 输出字符串
print("Hello, World!")

# 输出变量
name = "Alice"
print(name)

# 输出多个值
print("姓名:", name)
print("年龄:", 25)
```

### 参数详解

```python
# sep 参数：指定分隔符
print("Hello", "World", sep="-")      # Hello-World
print("2024", "01", "01", sep="/")     # 2024/01/01

# end 参数：指定结尾字符
print("Hello", end=" ")
print("World")                         # Hello World

# 不换行输出
for i in range(5):
    print(i, end=" ")                  # 0 1 2 3 4 
print()  # 换行
```

### 格式化输出

```python
# 使用 f-string
name = "Alice"
age = 25
print(f"姓名: {name}, 年龄: {age}")

# 使用 format()
print("姓名: {}, 年龄: {}".format(name, age))

# 使用 % 运算符
print("姓名: %s, 年龄: %d" % (name, age))
```

### 输出到文件

```python
# 输出到文件
with open("output.txt", "w") as f:
    print("Hello, File!", file=f)
    print("第二行", file=f)
```

### 输出颜色文本（ANSI 转义码）

```python
# 颜色输出（终端支持时）
print("\033[31m红色文本\033[0m")
print("\033[32m绿色文本\033[0m")
print("\033[34m蓝色文本\033[0m")
```

## 输入：input() 函数

### 基本输入

```python
# 获取用户输入
name = input("请输入你的名字: ")
print(f"你好, {name}!")

# 输入总是返回字符串
age = input("请输入你的年龄: ")
print(type(age))  # <class 'str'>
```

### 类型转换

```python
# 转换为整数
age = int(input("请输入你的年龄: "))
print(f"明年你{age + 1}岁")

# 转换为浮点数
height = float(input("请输入你的身高(米): "))
print(f"你的身高是{height}米")

# 转换为布尔值（需要特殊处理）
answer = input("是否继续? (y/n): ")
continue_flag = answer.lower() in ('y', 'yes', 'true', '1')
```

### 多值输入

```python
# 使用 split() 分割输入
x, y = input("请输入两个数字(空格分隔): ").split()
x, y = int(x), int(y)
print(f"和: {x + y}")

# 一行输入多个值
data = input("请输入姓名和年龄(空格分隔): ").split()
name = data[0]
age = int(data[1])
```

### 安全输入

```python
# 使用 try-except 处理无效输入
while True:
    try:
        age = int(input("请输入你的年龄: "))
        if age < 0:
            print("年龄不能为负数，请重新输入")
            continue
        break
    except ValueError:
        print("请输入有效的数字")

print(f"你的年龄是: {age}")
```

## 文件操作

### 读取文件

```python
# 读取整个文件
with open("file.txt", "r") as f:
    content = f.read()
    print(content)

# 逐行读取
with open("file.txt", "r") as f:
    for line in f:
        print(line.strip())

# 读取所有行到列表
with open("file.txt", "r") as f:
    lines = f.readlines()
    print(lines)
```

### 写入文件

```python
# 写入文件
with open("output.txt", "w") as f:
    f.write("Hello, World!\n")
    f.write("第二行\n")

# 使用 print() 写入
with open("output.txt", "w") as f:
    print("Hello, World!", file=f)
    print("第二行", file=f)
```

### 追加内容

```python
# 追加模式
with open("log.txt", "a") as f:
    f.write("新的日志内容\n")
```

## 格式化输出表格

```python
# 简单表格
data = [
    ["姓名", "年龄", "城市"],
    ["Alice", 25, "北京"],
    ["Bob", 30, "上海"],
    ["Charlie", 35, "广州"]
]

for row in data:
    print(f"{row[0]:<10} {row[1]:<5} {row[2]:<10}")
```

## 重定向输出

```python
import sys

# 重定向到文件
original_stdout = sys.stdout
with open("output.txt", "w") as f:
    sys.stdout = f
    print("这将写入文件")
    print("而不是显示在屏幕上")
sys.stdout = original_stdout

print("这将显示在屏幕上")
```

## 实际应用示例

### 简单计算器

```python
def calculator():
    print("简单计算器")
    print("----------")
    
    num1 = float(input("输入第一个数字: "))
    operator = input("输入运算符(+, -, *, /): ")
    num2 = float(input("输入第二个数字: "))
    
    if operator == "+":
        result = num1 + num2
    elif operator == "-":
        result = num1 - num2
    elif operator == "*":
        result = num1 * num2
    elif operator == "/":
        if num2 == 0:
            print("错误：除数不能为零")
            return
        result = num1 / num2
    else:
        print("无效的运算符")
        return
    
    print(f"{num1} {operator} {num2} = {result}")

calculator()
```

### 用户注册表单

```python
def register_user():
    print("用户注册")
    print("--------")
    
    username = input("用户名: ")
    email = input("邮箱: ")
    
    while True:
        password = input("密码: ")
        confirm = input("确认密码: ")
        if password == confirm:
            break
        print("密码不匹配，请重新输入")
    
    print(f"\n注册成功！")
    print(f"用户名: {username}")
    print(f"邮箱: {email}")

register_user()
```

### 读取 CSV 数据

```python
import csv

def read_csv(filename):
    with open(filename, "r", encoding="utf-8") as f:
        reader = csv.reader(f)
        for row in reader:
            print(", ".join(row))

# read_csv("data.csv")
```

## 调试输出

```python
# 使用 repr() 查看原始表示
text = "Hello\nWorld"
print(repr(text))  # 'Hello\\nWorld'

# 调试信息
x = 42
print(f"DEBUG: x = {x}")
print(f"DEBUG: type(x) = {type(x)}")
```
