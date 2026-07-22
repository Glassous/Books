# 嵌套循环

嵌套循环是指一个循环内部包含另一个循环。外层循环每执行一次，内层循环会完整执行一轮。

## for 嵌套

### 二维遍历

```python
# 遍历二维列表
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

### 九九乘法表

```python
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f"{j}x{i}={i*j}", end="\t")
    print()
```

### 打印三角形

```python
# 直角三角形
n = 5
for i in range(1, n + 1):
    for j in range(i):
        print("*", end="")
    print()
```

### 打印菱形

```python
n = 5
# 上半部分
for i in range(1, n + 1):
    for j in range(n - i):
        print(" ", end="")
    for k in range(2 * i - 1):
        print("*", end="")
    print()
# 下半部分
for i in range(n - 1, 0, -1):
    for j in range(n - i):
        print(" ", end="")
    for k in range(2 * i - 1):
        print("*", end="")
    print()
```

## while 嵌套

```python
# 使用 while 实现乘法表
i = 1
while i <= 9:
    j = 1
    while j <= i:
        print(f"{j}x{i}={i*j}", end="\t")
        j += 1
    print()
    i += 1
```

## for 与 while 混合嵌套

```python
# 查找质数
for n in range(2, 50):
    i = 2
    is_prime = True
    while i * i <= n:
        if n % i == 0:
            is_prime = False
            break
        i += 1
    if is_prime:
        print(n, end=" ")
print()  # 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47
```

## break 在嵌套循环中的作用

`break` 只跳出当前所在的最内层循环：

```python
# break 只跳出内层循环
for i in range(3):
    print(f"外层: {i}")
    for j in range(3):
        if j == 1:
            break  # 只跳出内层循环
        print(f"  内层: {j}")
```

### 使用标志变量跳出所有循环

```python
# 方式一：使用标志变量
found = False
for i in range(5):
    for j in range(5):
        if i == 2 and j == 2:
            found = True
            break
        print(f"({i}, {j})", end=" ")
    if found:
        break
    print()

# 方式二：使用 else + continue
for i in range(5):
    for j in range(5):
        if i == 2 and j == 2:
            print(f"\n找到目标: ({i}, {j})")
            break
        print(f"({i}, {j})", end=" ")
    else:
        continue
    break
```

## continue 在嵌套循环中

```python
# continue 跳过内层循环当前迭代
for i in range(3):
    print(f"外层: {i}")
    for j in range(3):
        if j == 1:
            continue
        print(f"  内层: {j}")
```

## 实际应用

### 矩阵转置

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6]
]

# 转置为 3x2 矩阵
transposed = []
for i in range(len(matrix[0])):
    new_row = []
    for j in range(len(matrix)):
        new_row.append(matrix[j][i])
    transposed.append(new_row)

print("原始矩阵:")
for row in matrix:
    print(row)
print("转置矩阵:")
for row in transposed:
    print(row)

# 使用列表推导式
transposed2 = [[matrix[j][i] for j in range(len(matrix))] for i in range(len(matrix[0]))]
```

### 杨辉三角

```python
def pascal_triangle(n):
    triangle = []
    for i in range(n):
        row = [1]
        if triangle:
            last_row = triangle[-1]
            for j in range(len(last_row) - 1):
                row.append(last_row[j] + last_row[j + 1])
            row.append(1)
        triangle.append(row)
    return triangle

def print_pascal(triangle):
    max_width = len(" ".join(map(str, triangle[-1])))
    for row in triangle:
        print(" ".join(map(str, row)).center(max_width))

print_pascal(pascal_triangle(6))
```

### 二维数组搜索

```python
def search_matrix(matrix, target):
    for i in range(len(matrix)):
        for j in range(len(matrix[i])):
            if matrix[i][j] == target:
                return (i, j)
    return None

matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

result = search_matrix(matrix, 5)
print(f"找到 5 在位置: {result}")  # (1, 1)
```

### 冒泡排序

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        swapped = False
        for j in range(n - 1 - i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr

numbers = [64, 34, 25, 12, 22, 11, 90]
print(f"排序前: {numbers}")
print(f"排序后: {bubble_sort(numbers)}")
```

### 生成坐标网格

```python
# 生成所有坐标
width, height = 3, 2
grid = []
for x in range(width):
    for y in range(height):
        grid.append((x, y))
print(grid)  # [(0, 0), (0, 1), (1, 0), (1, 1), (2, 0), (2, 1)]

# 使用列表推导式
grid2 = [(x, y) for x in range(width) for y in range(height)]
```

### 字符串匹配

```python
def find_substring(text, pattern):
    for i in range(len(text) - len(pattern) + 1):
        match = True
        for j in range(len(pattern)):
            if text[i + j] != pattern[j]:
                match = False
                break
        if match:
            return i
    return -1

text = "Hello, World!"
pattern = "World"
print(f"'{pattern}' 在位置: {find_substring(text, pattern)}")  # 7
```

## 嵌套循环性能考虑

```python
import time

# 外层循环次数少，内层循环次数多
n, m = 10, 1000000

start = time.time()
for i in range(n):
    for j in range(m):
        pass
print(f"外少内多: {time.time() - start:.2f}s")

# 外层循环次数多，内层循环次数少
start = time.time()
for i in range(m):
    for j in range(n):
        pass
print(f"外多内少: {time.time() - start:.2f}s")
```

## 限制嵌套层级

```python
# 避免过深嵌套，建议不超过 3 层
# 不推荐
# for a in ...:
#     for b in ...:
#         for c in ...:
#             for d in ...:
#                 pass  # 4 层嵌套

# 推荐：拆分为函数
def process_a(a):
    for b in ...:
        process_b(b)

def process_b(b):
    for c in ...:
        pass
```
