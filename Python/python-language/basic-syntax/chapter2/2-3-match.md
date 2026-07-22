# match

`match` 语句是 Python 3.10+ 引入的模式匹配语法，用于更简洁地处理多个条件分支。

## 基本语法

```python
match value:
    case pattern1:
        statement_block_1
    case pattern2:
        statement_block_2
    case _:
        default_block
```

## 匹配字面量

```python
def get_weekday(day):
    match day:
        case 1:
            return "星期一"
        case 2:
            return "星期二"
        case 3:
            return "星期三"
        case 4:
            return "星期四"
        case 5:
            return "星期五"
        case 6:
            return "星期六"
        case 7:
            return "星期日"
        case _:
            return "无效日期"

print(get_weekday(3))  # 星期三
print(get_weekday(8))  # 无效日期
```

## 匹配字符串

```python
def http_status(code):
    match code:
        case "200":
            return "成功"
        case "404":
            return "未找到"
        case "500":
            return "服务器错误"
        case _:
            return "未知状态"

print(http_status("404"))  # 未找到
```

## 匹配多个值

### 使用 |

```python
def vowel_or_consonant(char):
    match char.lower():
        case "a" | "e" | "i" | "o" | "u":
            return "元音"
        case _:
            return "辅音"

print(vowel_or_consonant("a"))  # 元音
print(vowel_or_consonant("b"))  # 辅音
```

### 使用列表匹配

```python
def process_command(command):
    match command.split():
        case ["quit"]:
            return "退出程序"
        case ["hello" | "hi", name]:
            return f"你好, {name}"
        case ["add", *items]:
            return f"添加: {items}"
        case _:
            return "未知命令"

print(process_command("quit"))          # 退出程序
print(process_command("hello Alice"))   # 你好, Alice
print(process_command("add apple banana")) # 添加: ['apple', 'banana']
```

## 匹配元组

```python
def process_point(point):
    match point:
        case (0, 0):
            return "原点"
        case (x, 0):
            return f"在 x 轴上, x={x}"
        case (0, y):
            return f"在 y 轴上, y={y}"
        case (x, y):
            return f"点 ({x}, {y})"
        case _:
            return "无效点"

print(process_point((0, 0)))     # 原点
print(process_point((5, 0)))     # 在 x 轴上, x=5
print(process_point((3, 4)))     # 点 (3, 4)
```

## 匹配时附带条件（Guard）

```python
def classify_number(n):
    match n:
        case n if n < 0:
            return "负数"
        case 0:
            return "零"
        case n if n % 2 == 0:
            return "正偶数"
        case _:
            return "正奇数"

print(classify_number(-5))  # 负数
print(classify_number(10))  # 正偶数
print(classify_number(7))   # 正奇数
```

## 匹配对象属性

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

def describe_point(point):
    match point:
        case Point(x=0, y=0):
            return "原点"
        case Point(x=x, y=y):
            return f"点 ({x}, {y})"
        case _:
            return "不是 Point 对象"

p = Point(3, 4)
print(describe_point(p))  # 点 (3, 4)
```

## 匹配字典

```python
def process_data(data):
    match data:
        case {"type": "text", "content": content}:
            return f"文本: {content}"
        case {"type": "image", "path": path}:
            return f"图片: {path}"
        case {"type": "video", "duration": d}:
            return f"视频时长: {d}秒"
        case _:
            return "未知数据类型"

print(process_data({"type": "text", "content": "Hello"}))    # 文本: Hello
print(process_data({"type": "image", "path": "/a.jpg"}))     # 图片: /a.jpg
```

## 匹配类型

```python
def describe_value(value):
    match value:
        case int(n):
            return f"整数: {n}"
        case float(f):
            return f"浮点数: {f}"
        case str(s):
            return f"字符串: {s}"
        case list(items):
            return f"列表: {items}"
        case dict(d):
            return f"字典: {d}"
        case _:
            return f"其他类型: {type(value).__name__}"

print(describe_value(42))            # 整数: 42
print(describe_value("hello"))       # 字符串: hello
print(describe_value([1, 2, 3]))     # 列表: [1, 2, 3]
```

## 通配符 _

```python
def match_example(value):
    match value:
        case 1:
            return "一"
        case 2:
            return "二"
        case _:
            # _ 匹配任何值，相当于 default
            return "其他数字"
```

## match 与 if-elif 对比

### 使用 if-elif

```python
def http_status_if(code):
    if code == 200:
        return "成功"
    elif code == 301:
        return "重定向"
    elif code == 404:
        return "未找到"
    elif code == 500:
        return "服务器错误"
    else:
        return "未知状态"
```

### 使用 match（更简洁）

```python
def http_status_match(code):
    match code:
        case 200:
            return "成功"
        case 301:
            return "重定向"
        case 404:
            return "未找到"
        case 500:
            return "服务器错误"
        case _:
            return "未知状态"
```

## 实际应用

### 简单解释器

```python
def simple_interpreter(command):
    match command.split():
        case ["print", *words]:
            return " ".join(words)
        case ["add", a, b]:
            return float(a) + float(b)
        case ["exit"] | ["quit"]:
            return None
        case _:
            return "未知命令"

print(simple_interpreter("print Hello World"))  # Hello World
print(simple_interpreter("add 10 20"))          # 30.0
```

### 形状计算器

```python
def calculate_area(shape):
    match shape:
        case ("circle", radius):
            return 3.14159 * radius ** 2
        case ("rectangle", w, h):
            return w * h
        case ("triangle", base, height):
            return 0.5 * base * height
        case _:
            return "未知形状"

print(calculate_area(("circle", 5)))       # 78.53975
print(calculate_area(("rectangle", 4, 5))) # 20
```
