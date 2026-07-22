# for 循环

`for` 循环用于遍历可迭代对象（如列表、字符串、字典等）。

## 基本语法

```python
for variable in iterable:
    statement_block
```

## 遍历序列

### 遍历列表

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

### 遍历元组

```python
point = (10, 20, 30)
for coord in point:
    print(coord)
```

### 遍历字符串

```python
for char in "Python":
    print(char, end=" ")
print()  # P y t h o n
```

## range() 函数

### 基本用法

```python
# range(stop)
for i in range(5):
    print(i, end=" ")  # 0 1 2 3 4
print()

# range(start, stop)
for i in range(2, 8):
    print(i, end=" ")  # 2 3 4 5 6 7
print()

# range(start, stop, step)
for i in range(0, 10, 2):
    print(i, end=" ")  # 0 2 4 6 8
print()

# 倒序
for i in range(10, 0, -1):
    print(i, end=" ")  # 10 9 8 7 6 5 4 3 2 1
print()
```

### 使用 range 遍历列表

```python
fruits = ["apple", "banana", "cherry"]

for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")
```

## 遍历字典

```python
person = {"name": "Alice", "age": 25, "city": "Beijing"}

# 遍历键
for key in person:
    print(key)  # name, age, city

# 遍历值
for value in person.values():
    print(value)  # Alice, 25, Beijing

# 遍历键值对
for key, value in person.items():
    print(f"{key}: {value}")
```

## 遍历集合并获得索引

### enumerate() 函数

```python
fruits = ["apple", "banana", "cherry"]

for i, fruit in enumerate(fruits):
    print(f"{i}: {fruit}")

# 指定起始索引
for i, fruit in enumerate(fruits, start=1):
    print(f"{i}. {fruit}")
```

## break 语句

```python
# 找到目标元素
numbers = [1, 3, 5, 7, 9, 11]
target = 7

for num in numbers:
    if num == target:
        print(f"找到 {target}")
        break
```

## continue 语句

```python
# 跳过偶数
for i in range(1, 11):
    if i % 2 == 0:
        continue
    print(i, end=" ")
print()  # 1 3 5 7 9

# 过滤特定值
data = [1, None, 3, None, 5]
valid = []
for item in data:
    if item is None:
        continue
    valid.append(item)
print(valid)  # [1, 3, 5]
```

## else 子句

当循环正常结束（未遇到 `break`）时执行 `else` 块：

```python
# 查找质数
def find_prime(numbers):
    for n in numbers:
        if n <= 1:
            continue
        for i in range(2, int(n ** 0.5) + 1):
            if n % i == 0:
                break
        else:
            print(f"{n} 是质数")

find_prime([10, 15, 17, 20, 23])
```

## 嵌套 for 循环

```python
# 九九乘法表
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f"{j}x{i}={i*j}", end="\t")
    print()

# 打印二维数组
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for row in matrix:
    for element in row:
        print(element, end=" ")
    print()
```

## 列表推导式

```python
# 基本列表推导式
squares = [x ** 2 for x in range(10)]
print(squares)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# 带条件
even_squares = [x ** 2 for x in range(10) if x % 2 == 0]
print(even_squares)  # [0, 4, 16, 36, 64]

# 嵌套循环
matrix = [[i * j for j in range(1, 4)] for i in range(1, 4)]
print(matrix)  # [[1, 2, 3], [2, 4, 6], [3, 6, 9]]

# 字符串操作
words = ["hello", "world", "python"]
upper_words = [w.upper() for w in words]
print(upper_words)  # ['HELLO', 'WORLD', 'PYTHON']
```

## 实际应用

### 求和

```python
numbers = [1, 2, 3, 4, 5]

total = 0
for num in numbers:
    total += num
print(f"总和: {total}")  # 15

# 使用 sum()
print(f"总和: {sum(numbers)}")  # 15
```

### 查找最大值

```python
numbers = [3, 7, 1, 9, 4, 6]

max_num = numbers[0]
for num in numbers:
    if num > max_num:
        max_num = num
print(f"最大值: {max_num}")  # 9

# 使用 max()
print(f"最大值: {max(numbers)}")  # 9
```

### 统计数据

```python
data = [85, 92, 78, 95, 88, 76, 90]

total = sum(data)
count = len(data)
average = total / count

above_avg = [x for x in data if x > average]

print(f"平均分: {average:.1f}")
print(f"高于平均分的人数: {len(above_avg)}")
print(f"最高分: {max(data)}")
print(f"最低分: {min(data)}")
```

### 字符串处理

```python
# 统计元音
text = "Hello, World! Python is awesome."
vowels = "aeiouAEIOU"
count = 0

for char in text:
    if char in vowels:
        count += 1

print(f"元音数量: {count}")  # 10
```

### 合并字典

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

merged = {}
for d in (dict1, dict2):
    for key, value in d.items():
        merged[key] = value

print(merged)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}
```

### 文件读取

```python
# 逐行读取文件
with open("example.txt", "r") as f:
    for line in f:
        print(line.strip())
```

## for 与 while 的选择

### 适合用 for 的场景

```python
# 遍历已知序列
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# 确定次数
for i in range(100):
    print(i)
```

### 适合用 while 的场景

```python
# 条件不确定
while True:
    user_input = input("输入 'quit' 退出: ")
    if user_input == "quit":
        break

# 需要条件控制
x = 100
while x > 1:
    x //= 2
    print(x)
```
