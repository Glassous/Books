# 赋值运算符

赋值运算符用于给变量赋值，Python 提供了多种赋值方式。

## 基本赋值（=）

```python
# 简单赋值
x = 10
name = "Alice"
pi = 3.14

# 同时赋值多个变量
x, y, z = 1, 2, 3
print(x, y, z)  # 1 2 3

# 同一值赋给多个变量
a = b = c = 0
print(a, b, c)  # 0 0 0

# 交换变量值
a, b = 10, 20
a, b = b, a
print(a, b)  # 20 10
```

## 增强赋值运算符

### 加法赋值（+=）

```python
x = 10
x += 5  # 等价于 x = x + 5
print(x)  # 15

# 字符串拼接
text = "Hello"
text += " World"
print(text)  # Hello World

# 列表扩展
numbers = [1, 2]
numbers += [3, 4]
print(numbers)  # [1, 2, 3, 4]
```

### 减法赋值（-=）

```python
x = 10
x -= 3  # 等价于 x = x - 3
print(x)  # 7
```

### 乘法赋值（*=）

```python
x = 5
x *= 3  # 等价于 x = x * 3
print(x)  # 15

# 字符串重复
text = "Ha"
text *= 3
print(text)  # HaHaHa

# 列表重复
numbers = [1, 2]
numbers *= 2
print(numbers)  # [1, 2, 1, 2]
```

### 除法赋值（/=）

```python
x = 15
x /= 3  # 等价于 x = x / 3
print(x)  # 5.0
```

### 整除赋值（//=）

```python
x = 17
x //= 3  # 等价于 x = x // 3
print(x)  # 5
```

### 取模赋值（%=）

```python
x = 17
x %= 3  # 等价于 x = x % 3
print(x)  # 2
```

### 幂赋值（**=）

```python
x = 2
x **= 3  # 等价于 x = x ** 3
print(x)  # 8
```

### 位运算赋值

```python
# 按位与赋值
x = 12  # 1100
x &= 10  # 1010
print(x)  # 8 (1000)

# 按位或赋值
x = 12  # 1100
x |= 5   # 0101
print(x)  # 13 (1101)

# 按位异或赋值
x = 12  # 1100
x ^= 5   # 0101
print(x)  # 9 (1001)

# 左移赋值
x = 5   # 101
x <<= 2
print(x)  # 20 (10100)

# 右移赋值
x = 20  # 10100
x >>= 2
print(x)  # 5 (101)
```

## 解包赋值

### 基本解包

```python
# 列表解包
numbers = [1, 2, 3]
a, b, c = numbers
print(a, b, c)  # 1 2 3

# 元组解包
point = (10, 20)
x, y = point
print(x, y)  # 10 20
```

### 星号解包

```python
# 获取剩余元素
numbers = [1, 2, 3, 4, 5]
first, *rest = numbers
print(first)  # 1
print(rest)   # [2, 3, 4, 5]

first, *middle, last = numbers
print(first)   # 1
print(middle)  # [2, 3, 4]
print(last)    # 5

# 字符串解包
s = "hello"
first, *rest = s
print(first)  # h
print(rest)   # ['e', 'l', 'l', 'o']
```

### 嵌套解包

```python
# 嵌套列表解包
data = [1, [2, 3], 4]
a, (b, c), d = data
print(a, b, c, d)  # 1 2 3 4

# 嵌套元组解包
point = (10, (20, 30))
x, (y, z) = point
print(x, y, z)  # 10 20 30
```

## 海象运算符（:=）

Python 3.8+ 引入的赋值表达式，可以在表达式中赋值。

```python
# 基本用法
if (n := len("hello")) > 3:
    print(f"长度{n}大于3")

# 在 while 循环中使用
import random
while (num := random.randint(1, 10)) != 5:
    print(f"生成了{num}，不是5")
print(f"终于生成了{num}")

# 在列表推导式中使用
numbers = [1, 2, 3, 4, 5]
results = [y for x in numbers if (y := x * 2) > 5]
print(results)  # [6, 8, 10]

# 在函数参数中使用
def process(text):
    return text.upper()

words = ["hello", "world", "python"]
processed = [result for word in words if (result := process(word)) != "HELLO"]
print(processed)  # ['WORLD', 'PYTHON']
```

## 链式赋值

```python
# 链式赋值
a = b = c = 10
print(a, b, c)  # 10 10 10

# 修改一个变量不影响其他
a = 20
print(a, b, c)  # 20 10 10

# 注意可变对象
list1 = list2 = [1, 2, 3]
list1.append(4)
print(list1)  # [1, 2, 3, 4]
print(list2)  # [1, 2, 3, 4]（同一个对象）
```

## 实际应用

### 计数器

```python
# 使用 += 计数
count = 0
for i in range(10):
    if i % 2 == 0:
        count += 1
print(f"偶数个数: {count}")  # 5
```

### 累加器

```python
# 使用 += 累加
total = 0
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    total += num
print(f"总和: {total}")  # 15
```

### 交换排序

```python
# 使用交换赋值排序
numbers = [64, 34, 25, 12, 22, 11, 90]

for i in range(len(numbers)):
    for j in range(i + 1, len(numbers)):
        if numbers[i] > numbers[j]:
            numbers[i], numbers[j] = numbers[j], numbers[i]

print(f"排序后: {numbers}")
```

### 条件赋值

```python
# 使用海象运算符
import random

# 生成随机数直到满足条件
numbers = []
while (num := random.randint(1, 100)) > 50:
    numbers.append(num)
print(f"生成的数: {numbers}")
print(f"最后的数: {num}")
```

## 注意事项

```python
# 未定义变量会报错
# print(undefined_var)  # NameError

# 增强赋值不可用于未定义变量
# x += 1  # NameError

# 可变对象的赋值是引用
list1 = [1, 2, 3]
list2 = list1
list2.append(4)
print(list1)  # [1, 2, 3, 4]（被修改）

# 使用 copy() 创建副本
list3 = list1.copy()
list3.append(5)
print(list1)  # [1, 2, 3, 4]（未被修改）
print(list3)  # [1, 2, 3, 4, 5]
```
