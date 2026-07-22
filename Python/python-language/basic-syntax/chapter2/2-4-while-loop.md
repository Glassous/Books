# while 循环

`while` 循环用于在条件为真时重复执行代码块。

## 基本语法

```python
while condition:
    statement_block
```

### 基本示例

```python
# 基本的 while 循环
count = 0
while count < 5:
    print(f"计数: {count}")
    count += 1
```

## 计数器循环

```python
# 从 1 数到 10
i = 1
while i <= 10:
    print(i, end=" ")
    i += 1
print()  # 1 2 3 4 5 6 7 8 9 10

# 倒计时
i = 10
while i > 0:
    print(i, end=" ")
    i -= 1
print("发射!")  # 10 9 8 7 6 5 4 3 2 1 发射!
```

## 无限循环

### while True

```python
# 无限循环（通常配合 break 使用）
while True:
    user_input = input("输入 'quit' 退出: ")
    if user_input == "quit":
        break
    print(f"你输入了: {user_input}")
```

### 条件永不满足避免死循环

```python
# 确保循环条件最终会变为 False
x = 10
while x > 0:
    print(x)
    x -= 1  # 确保循环终止
```

## break 语句

```python
# 找到第一个偶数
n = 1
while True:
    if n % 7 == 0 and n % 5 == 0:
        print(f"第一个能被5和7整除的数是: {n}")
        break
    n += 1
```

## continue 语句

```python
# 跳过偶数
n = 0
while n < 10:
    n += 1
    if n % 2 == 0:
        continue
    print(n, end=" ")
print()  # 1 3 5 7 9
```

## else 子句

当循环正常结束（未遇到 `break`）时执行 `else` 块：

```python
# 查找数字
def find_number(numbers, target):
    i = 0
    while i < len(numbers):
        if numbers[i] == target:
            print(f"找到 {target}")
            break
        i += 1
    else:
        print(f"未找到 {target}")

find_number([1, 3, 5, 7, 9], 5)  # 找到 5
find_number([1, 3, 5, 7, 9], 2)  # 未找到 2
```

## 循环控制组合

```python
# 处理用户输入
def process_numbers():
    numbers = []
    while True:
        user_input = input("输入数字（或 'done' 结束）: ")
        if user_input == "done":
            break
        if not user_input.isdigit():
            print("请输入有效数字")
            continue
        numbers.append(int(user_input))

    if numbers:
        print(f"输入的数字: {numbers}")
        print(f"最大值: {max(numbers)}")
        print(f"最小值: {min(numbers)}")
        print(f"总和: {sum(numbers)}")
    else:
        print("未输入任何数字")
```

## 实际应用

### 猜数字游戏

```python
import random

def guess_number():
    secret = random.randint(1, 100)
    attempts = 0

    print("猜数字游戏 (1-100)")
    while True:
        try:
            guess = int(input("请输入猜测: "))
            attempts += 1

            if guess < secret:
                print("太小了")
            elif guess > secret:
                print("太大了")
            else:
                print(f"恭喜！猜对了！用了 {attempts} 次")
                break
        except ValueError:
            print("请输入有效数字")
```

### 计算平方根（牛顿迭代法）

```python
def sqrt_newton(n, precision=1e-10):
    if n < 0:
        return None
    if n == 0:
        return 0

    x = n
    while True:
        next_x = (x + n / x) / 2
        if abs(next_x - x) < precision:
            return next_x
        x = next_x

print(sqrt_newton(16))   # 4.0
print(sqrt_newton(2))    # 1.414213562373095
```

### 斐波那契数列

```python
def fibonacci(n):
    a, b = 0, 1
    count = 0
    while count < n:
        print(a, end=" ")
        a, b = b, a + b
        count += 1
    print()

fibonacci(10)  # 0 1 1 2 3 5 8 13 21 34
```

### 数字反转

```python
def reverse_number(n):
    result = 0
    original = n

    while n > 0:
        remainder = n % 10
        result = result * 10 + remainder
        n //= 10

    return result

print(reverse_number(12345))  # 54321
print(reverse_number(1000))   # 1
```

### 质数判断

```python
def is_prime(n):
    if n <= 1:
        return False

    i = 2
    while i * i <= n:
        if n % i == 0:
            return False
        i += 1
    return True

# 找出 1-50 的质数
n = 2
while n <= 50:
    if is_prime(n):
        print(n, end=" ")
    n += 1
print()  # 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47
```

### 密码验证

```python
def password_check():
    password = "python123"
    attempts = 0
    max_attempts = 3

    while attempts < max_attempts:
        user_input = input("请输入密码: ")
        attempts += 1

        if user_input == password:
            print("登录成功")
            return True
        else:
            remaining = max_attempts - attempts
            if remaining > 0:
                print(f"密码错误，还剩 {remaining} 次机会")

    print("登录失败，已达最大尝试次数")
    return False
```

## 常见错误

```python
# 错误：忘记修改循环变量（死循环）
# i = 0
# while i < 10:
#     print(i)
#     # 忘记 i += 1

# 错误：条件写反
# while True:  # 不是 False
#     break

# 错误：无限循环
# while 1:  # 1 始终为真
#     print("无限循环")
#     break
```
