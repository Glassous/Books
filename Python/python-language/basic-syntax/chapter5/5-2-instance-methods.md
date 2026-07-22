# 实例方法

实例方法（Instance Method）是定义在类中、通过实例调用的函数，第一个参数必须是 `self`。

## 定义实例方法

```python
class Calculator:
    def add(self, a, b):
        return a + b

    def subtract(self, a, b):
        return a - b

calc = Calculator()
print(calc.add(10, 5))       # 15
print(calc.subtract(10, 5))  # 5
```

## 方法调用本质

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(f"{self.name}: 汪汪！")

dog = Dog("旺财")

# 方式一：通过实例调用
dog.bark()  # 旺财: 汪汪！

# 方式二：通过类调用（手动传 self）
Dog.bark(dog)  # 旺财: 汪汪！
```

## 带返回值的方法

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

    def perimeter(self):
        return 2 * 3.14159 * self.radius

c = Circle(5)
print(f"面积: {c.area():.2f}")       # 78.54
print(f"周长: {c.perimeter():.2f}")  # 31.42
```

## 方法链式调用

```python
class StringUtils:
    def __init__(self):
        self.text = ""

    def set_text(self, text):
        self.text = text
        return self  # 返回 self 实现链式调用

    def add_prefix(self, prefix):
        self.text = prefix + self.text
        return self

    def add_suffix(self, suffix):
        self.text = self.text + suffix
        return self

    def to_upper(self):
        self.text = self.text.upper()
        return self

    def result(self):
        return self.text

s = StringUtils()
result = s.set_text("hello").add_prefix(">> ").add_suffix(" <<").to_upper().result()
print(result)  # >> HELLO <<
```

## 方法与函数对比

```python
# 普通函数
def greet(name):
    return f"Hello, {name}"

print(greet("Alice"))  # Hello, Alice

# 实例方法
class Person:
    def __init__(self, name):
        self.name = name

    def greet(self):
        return f"Hello, {self.name}"

p = Person("Bob")
print(p.greet())  # Hello, Bob
```

## 调用其他方法

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            self._log(f"存款 {amount}")
        return self.balance

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            self._log(f"取款 {amount}")
        return self.balance

    def _log(self, message):
        """内部方法（以 _ 开头表示私有）"""
        print(f"[{self.owner}] {message}，余额: {self.balance}")

account = BankAccount("Alice", 1000)
account.deposit(500)    # [Alice] 存款 500，余额: 1500
account.withdraw(200)   # [Alice] 取款 200，余额: 1300
```
