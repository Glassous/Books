# 算术运算符

算术运算符用于执行基本的数学运算。

## 基本算术运算符

### 加法（+）

```python
# 整数加法
result = 10 + 5
print(result)  # 15

# 浮点数加法
result = 3.14 + 2.86
print(result)  # 6.0

# 字符串拼接（特殊用法）
text = "Hello" + " " + "World"
print(text)  # Hello World
```

### 减法（-）

```python
# 整数减法
result = 10 - 5
print(result)  # 5

# 浮点数减法
result = 3.14 - 1.14
print(result)  # 2.0

# 负数
result = -10
print(result)  # -10
```

### 乘法（*）

```python
# 整数乘法
result = 10 * 5
print(result)  # 50

# 浮点数乘法
result = 3.14 * 2
print(result)  # 6.28

# 字符串重复（特殊用法）
text = "Ha" * 3
print(text)  # HaHaHa

# 列表重复
numbers = [1, 2] * 3
print(numbers)  # [1, 2, 1, 2, 1, 2]
```

### 除法（/）

```python
# 除法总是返回浮点数
result = 10 / 3
print(result)  # 3.3333333333333335

result = 10 / 2
print(result)  # 5.0

# 注意：即使能整除，结果也是浮点数
result = 10 / 5
print(result)  # 2.0
```

### 整除（//）

```python
# 整除返回向下取整的整数
result = 10 // 3
print(result)  # 3

result = 10 // 2
print(result)  # 5

# 负数整除
result = -10 // 3
print(result)  # -4（向下取整）

# 浮点数整除
result = 10.5 // 3
print(result)  # 3.0
```

### 取模（%）

```python
# 取模返回除法的余数
result = 10 % 3
print(result)  # 1

result = 10 % 2
print(result)  # 0

# 判断奇偶数
num = 7
if num % 2 == 0:
    print(f"{num}是偶数")
else:
    print(f"{num}是奇数")

# 浮点数取模
result = 10.5 % 3
print(result)  # 1.5
```

### 幂运算（**）

```python
# 幂运算
result = 2 ** 3
print(result)  # 8

result = 10 ** 2
print(result)  # 100

# 开方
result = 9 ** 0.5
print(result)  # 3.0

# 负指数
result = 2 ** -1
print(result)  # 0.5
```

## 运算符优先级

从高到低：
1. `**`（幂运算）
2. `+x`, `-x`, `~x`（一元运算符）
3. `*`, `/`, `//`, `%`（乘除）
4. `+`, `-`（加减）

```python
# 优先级示例
result = 2 + 3 * 4
print(result)  # 14（先乘后加）

result = (2 + 3) * 4
print(result)  # 20（括号优先）

result = 2 ** 3 ** 2
print(result)  # 512（右结合：2**(3**2) = 2**9）

result = 2 * 3 ** 2
print(result)  # 18（幂运算优先：2*(3**2)）
```

## 数学函数

### 内置函数

```python
# 绝对值
print(abs(-10))  # 10

# 最大值和最小值
print(max(1, 2, 3, 4, 5))  # 5
print(min(1, 2, 3, 4, 5))  # 1

# 求和
numbers = [1, 2, 3, 4, 5]
print(sum(numbers))  # 15

# 商和余数
quotient, remainder = divmod(10, 3)
print(f"商: {quotient}, 余数: {remainder}")  # 商: 3, 余数: 1

# 四舍五入
print(round(3.14159, 2))  # 3.14
print(round(3.5))  # 4
```

### math 模块

```python
import math

# 向上取整和向下取整
print(math.ceil(3.2))   # 4
print(math.floor(3.8))  # 3

# 开方
print(math.sqrt(16))  # 4.0

# 对数
print(math.log(100, 10))  # 2.0
print(math.log2(8))       # 3.0
print(math.log10(100))    # 2.0

# 常量
print(math.pi)   # 3.141592653589793
print(math.e)    # 2.718281828459045

# 三角函数
print(math.sin(math.pi / 2))  # 1.0
print(math.cos(0))            # 1.0
print(math.tan(math.pi / 4))  # 0.9999999999999999

# 阶乘
print(math.factorial(5))  # 120
```

## 类型转换

```python
# 整数运算
result = 10 + 5  # int + int = int
print(type(result))  # <class 'int'>

# 浮点数运算
result = 10 + 5.0  # int + float = float
print(type(result))  # <class 'float'>

# 混合运算
result = 10 / 3  # 总是返回 float
print(type(result))  # <class 'float'>

# 强制转换
result = int(10 / 3)  # 截断小数
print(result)  # 3
```

## 实际应用

### 计算圆的面积和周长

```python
import math

radius = float(input("请输入圆的半径: "))

area = math.pi * radius ** 2
circumference = 2 * math.pi * radius

print(f"面积: {area:.2f}")
print(f"周长: {circumference:.2f}")
```

### 温度转换

```python
def celsius_to_fahrenheit(celsius):
    return celsius * 9/5 + 32

def fahrenheit_to_celsius(fahrenheit):
    return (fahrenheit - 32) * 5/9

# 使用示例
c = 25
f = celsius_to_fahrenheit(c)
print(f"{c}°C = {f}°F")

f = 77
c = fahrenheit_to_celsius(f)
print(f"{f}°F = {c:.1f}°C")
```

### 复利计算

```python
def compound_interest(principal, rate, time):
    """计算复利"""
    amount = principal * (1 + rate) ** time
    interest = amount - principal
    return amount, interest

# 使用示例
principal = 10000  # 本金
rate = 0.05        # 年利率 5%
time = 5           # 5年

amount, interest = compound_interest(principal, rate, time)
print(f"本金: {principal}")
print(f"年利率: {rate*100}%")
print(f"时间: {time}年")
print(f"最终金额: {amount:.2f}")
print(f"利息: {interest:.2f}")
```

### 数字各位之和

```python
def digit_sum(n):
    """计算数字各位之和"""
    n = abs(n)
    total = 0
    while n > 0:
        total += n % 10
        n //= 10
    return total

# 使用示例
num = 12345
print(f"{num} 的各位数字之和: {digit_sum(num)}")  # 15
```

## 注意事项

```python
# 除以零错误
# result = 10 / 0  # ZeroDivisionError

# 幂运算的特殊情况
print(0 ** 0)  # 1（数学定义）

# 浮点数精度问题
print(0.1 + 0.2)  # 0.30000000000000004

# 使用 decimal 模块处理精确计算
from decimal import Decimal
print(Decimal('0.1') + Decimal('0.2'))  # 0.3
```
