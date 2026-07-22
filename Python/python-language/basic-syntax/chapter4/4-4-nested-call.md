# 函数嵌套调用

函数嵌套调用是指在一个函数中调用另一个函数，这是编程中最常见的组合方式。

## 基本嵌套调用

```python
def square(x):
    return x * x

def sum_of_squares(a, b):
    return square(a) + square(b)

print(sum_of_squares(3, 4))  # 25（3² + 4²）
```

## 多层嵌套

```python
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

def calculate(x, y, z):
    return multiply(add(x, y), z)

print(calculate(2, 3, 4))  # 20（(2+3) × 4）
```

## 函数链式调用

函数的返回值直接作为另一个函数的参数：

```python
def double(x):
    return x * 2

def add_one(x):
    return x + 1

def to_string(x):
    return str(x)

result = to_string(add_one(double(5)))
print(result)  # "11"（(((5×2)+1) 转字符串）
```

## 内部辅助函数

在函数内定义辅助函数，仅在该函数内部使用：

```python
def process_data(data):
    def clean(value):
        """内部辅助函数：清理数据"""
        return value.strip().lower()

    def validate(value):
        """内部辅助函数：验证数据"""
        return len(value) > 0

    result = []
    for item in data:
        cleaned = clean(item)
        if validate(cleaned):
            result.append(cleaned)
    return result

data = [" Hello ", "WORLD", " ", "Python"]
print(process_data(data))  # ['hello', 'world', 'python']
```

## 实际应用示例

### 温度转换工具

```python
def celsius_to_fahrenheit(c):
    """摄氏转华氏"""
    return c * 9 / 5 + 32

def fahrenheit_to_celsius(f):
    """华氏转摄氏"""
    return (f - 32) * 5 / 9

def convert_temperature(value, from_unit, to_unit):
    """温度转换器"""
    if from_unit == to_unit:
        return value
    if from_unit == "C" and to_unit == "F":
        return celsius_to_fahrenheit(value)
    if from_unit == "F" and to_unit == "C":
        return fahrenheit_to_celsius(value)
    return "不支持的单位"

print(convert_temperature(100, "C", "F"))  # 212.0
print(convert_temperature(32, "F", "C"))   # 0.0
```

### 字符串处理管道

```python
def remove_punctuation(text):
    """移除标点符号"""
    import string
    return "".join(ch for ch in text if ch not in string.punctuation)

def split_words(text):
    """分词"""
    return text.split()

def count_words(words):
    """统计词频"""
    from collections import Counter
    return Counter(words)

def analyze_text(text):
    """文本分析管道"""
    cleaned = remove_punctuation(text)
    words = split_words(cleaned)
    return count_words(words)

text = "Hello, world! Hello, Python! Python is great."
result = analyze_text(text)
print(result)  # Counter({'Hello': 2, 'world': 1, 'Python': 2, 'is': 1, 'great': 1})
```
