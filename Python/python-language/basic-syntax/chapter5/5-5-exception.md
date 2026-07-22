# 异常

异常（Exception）是程序运行过程中发生的错误。Python 提供了异常处理机制来捕获和处理这些错误。

## try-except

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("除数不能为 0")
```

## 捕获多个异常

```python
try:
    num = int(input("请输入数字: "))
    result = 10 / num
except ValueError:
    print("请输入有效数字")
except ZeroDivisionError:
    print("除数不能为 0")
```

## 捕获所有异常

```python
try:
    x = int("abc")
except Exception as e:
    print(f"发生错误: {e}")
```

## else 与 finally

```python
try:
    num = int(input("请输入数字: "))
    result = 10 / num
except ValueError:
    print("请输入有效数字")
except ZeroDivisionError:
    print("除数不能为 0")
else:
    print(f"计算成功: {result}")
finally:
    print("无论是否出错都会执行")
```

## 自定义异常

```python
class BalanceError(Exception):
    """余额异常"""
    pass

class InsufficientBalanceError(BalanceError):
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        super().__init__(f"余额不足：需 {amount}，仅 {balance}")
```

## raise 抛出异常

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance

    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("取款金额必须为正数")
        if amount > self.balance:
            raise InsufficientBalanceError(self.balance, amount)
        self.balance -= amount

account = BankAccount("Alice", 1000)

try:
    account.withdraw(2000)
except InsufficientBalanceError as e:
    print(e)  # 余额不足：需 2000，仅 1000
```

## 常见内置异常

```python
# ValueError：参数值错误
# int("abc")

# TypeError：类型错误
# "hello" + 123

# IndexError：索引越界
# [1, 2, 3][10]

# KeyError：键不存在
# {"a": 1}["b"]

# FileNotFoundError：文件不存在
# open("nonexistent.txt")

# AttributeError：属性不存在
# "hello".unknown_method()
```

## 异常处理最佳实践

```python
# 只捕获预期的异常
try:
    num = int(input("数字: "))
except ValueError:
    print("输入无效")

# 避免捕获后沉默
try:
    result = risky_operation()
except Exception:
    pass  # 不要这样做

# 使用 finally 释放资源
file = None
try:
    file = open("data.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("文件不存在")
finally:
    if file:
        file.close()

# 使用 with 语句简化资源管理
try:
    with open("data.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("文件不存在")
```
