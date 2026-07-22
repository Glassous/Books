# 第五章 汇总

本章汇总了面向对象编程的核心知识点，包含速览、示例代码和完整示例文件。

---

## 速览

### 5.1 类与对象
- `class` 关键字定义类
- 对象是类的实例：`obj = ClassName()`
- `__init__` 构造方法初始化属性
- `self` 指向实例本身

### 5.2 实例方法
- 实例方法第一个参数是 `self`
- 通过实例调用：`obj.method()`
- 通过类调用：`ClassName.method(obj)`
- 可返回 `self` 实现链式调用

### 5.3 魔方方法
- `__init__`：构造方法
- `__str__` / `__repr__`：字符串表示
- `__len__`：`len()` 函数
- `__add__`：`+` 运算符
- `__eq__` / `__lt__`：比较运算符
- `__getitem__`：索引访问
- `__call__`：使实例可调用

### 5.4 实例属性与类属性
- 实例属性：通过 `self` 定义，每个实例独立
- 类属性：在类中直接定义，所有实例共享
- 实例属性优先于类属性
- `@property` 装饰器将方法转为属性（getter/setter/deleter）
- 计算属性：`@property` 实现实时计算
- 缓存属性：通过缓存避免重复计算
- 数据验证：setter 中验证输入
- `_` 单下划线约定保护，`__` 双下划线名称修饰

### 5.5 @classmethod 与 @staticmethod
- `@classmethod`：接收类参数 `cls`，可访问类属性
- `@staticmethod`：不接收类或实例，类似普通函数
- 工厂方法：`@classmethod` 从不同输入创建实例
- 工具方法：`@staticmethod` 组织相关功能

### 5.6 继承与多态
- 基本继承：`class B(A)` 子类获取父类属性和方法
- `super()`：调用父类方法
- 方法重写：子类覆盖或扩展父类方法
- 多态：不同类的对象响应相同接口
- `isinstance()` / `issubclass()`：类型检查
- 多继承：一个类继承多个父类（MRO）
- 抽象基类：`ABC` + `@abstractmethod` 定义接口规范

### 5.7 异常
- `try-except` 捕获异常
- `else` 无异常时执行，`finally` 始终执行
- 自定义异常继承 `Exception`
- `raise` 主动抛出异常
- 使用 `with` 语句简化资源管理

### 5.8 案例：银行账户管理系统
- 账户基类：存款、取款、转账、交易记录
- 储蓄账户：利率计算、存款期限
- 信用卡：透支额度、手续费
- 银行类：开户、转账、账户管理
- 完整运用魔方方法和异常处理

---

## 示例代码

### 类定义与使用

```python
class Student:
    school = "第一中学"  # 类属性

    def __init__(self, name, score):
        self.name = name      # 实例属性
        self.score = score

    def introduce(self):
        print(f"我叫{self.name}，成绩{self.score}分")

    def __str__(self):
        return f"{self.name}({self.score}分)"

s1 = Student("Alice", 95)
s1.introduce()
print(s1)
print(s1.school)
```

### 异常处理

```python
class BalanceError(Exception):
    pass

try:
    amount = float(input("取款金额: "))
    if amount <= 0:
        raise ValueError("金额必须为正")
    if amount > 1000:
        raise BalanceError("余额不足")
except ValueError as e:
    print(f"输入错误: {e}")
except BalanceError as e:
    print(f"业务错误: {e}")
except Exception as e:
    print(f"未知错误: {e}")
else:
    print(f"取款 {amount} 成功")
finally:
    print("交易结束")
```

### 魔方方法

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

    def __str__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = Vector(1, 2)

print(v1 + v2)  # Vector(4, 6)
print(v1 == v3)  # True
```

---

## 完整示例文件

```python
"""
第五章 面向对象基础 - 综合示例
包含：类与对象、实例方法、魔方方法、属性、异常处理
"""

# ============================================
# 1. 类基础
# ============================================
print("=" * 50)
print("1. 类基础")
print("=" * 50)

class Dog:
    species = "犬科"

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def bark(self):
        return f"{self.name}: 汪汪！"

    def __str__(self):
        return f"{self.name}({self.age}岁)"

dog1 = Dog("旺财", 3)
dog2 = Dog("来福", 5)

print(f"{dog1} - {dog1.bark()}")
print(f"{dog2} - {dog2.bark()}")
print(f"物种: {dog1.species}, {dog2.species}")

# ============================================
# 2. 魔方方法
# ============================================
print("\n" + "=" * 50)
print("2. 魔方方法")
print("=" * 50)

class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages

    def __str__(self):
        return f"《{self.title}》- {self.author}"

    def __repr__(self):
        return f"Book('{self.title}', '{self.author}', {self.pages})"

    def __len__(self):
        return self.pages

    def __eq__(self, other):
        return self.title == other.title and self.author == other.author

    def __contains__(self, keyword):
        return keyword in self.title or keyword in self.author

book1 = Book("Python编程", "Alice", 300)
book2 = Book("数据结构", "Bob", 250)
book3 = Book("Python编程", "Alice", 300)

print(book1)
print(repr(book2))
print(f"页数: {len(book1)}")
print(f"book1 == book3: {book1 == book3}")
print(f"'Python' in book1: {'Python' in book1}")

# ============================================
# 3. 属性
# ============================================
print("\n" + "=" * 50)
print("3. 属性")
print("=" * 50)

class Counter:
    count = 0

    def __init__(self, name):
        self.name = name
        Counter.count += 1

    @property
    def info(self):
        return f"{self.name} (第{self.__class__.count}个)"

c1 = Counter("A")
c2 = Counter("B")
c3 = Counter("C")

print(f"实例总数: {Counter.count}")
print(f"c1.info: {c1.info}")
print(f"c3.info: {c3.info}")

# ============================================
# 4. 异常处理
# ============================================
print("\n" + "=" * 50)
print("4. 异常处理")
print("=" * 50)

def divide_safe(a, b):
    try:
        result = a / b
    except ZeroDivisionError:
        return "除数不能为 0"
    except TypeError:
        return "参数必须是数字"
    else:
        return result
    finally:
        print(f"  divide_safe({a}, {b}) 调用完成")

print(f"10 / 2 = {divide_safe(10, 2)}")
print(f"10 / 0 = {divide_safe(10, 0)}")
print(f"10 / 'a' = {divide_safe(10, 'a')}")

# 自定义异常
class AgeError(Exception):
    def __init__(self, age, message=None):
        self.age = age
        if message is None:
            message = f"年龄无效: {age}"
        super().__init__(message)

def set_age(age):
    if not isinstance(age, int):
        raise TypeError("年龄必须是整数")
    if age < 0 or age > 150:
        raise AgeError(age)
    return f"年龄设置为 {age}"

try:
    print(set_age(25))
    print(set_age(-5))
except AgeError as e:
    print(f"错误: {e}")

# ============================================
# 5. 银行系统演示
# ============================================
print("\n" + "=" * 50)
print("5. 银行系统演示")
print("=" * 50)

class BankError(Exception):
    pass

class Account:
    bank_name = "Python 银行"

    def __init__(self, owner, balance=0):
        self.owner = owner
        self._balance = balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("存款金额必须为正")
        self._balance += amount
        return self._balance

    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("取款金额必须为正")
        if amount > self._balance:
            raise BankError("余额不足")
        self._balance -= amount
        return self._balance

    @property
    def balance(self):
        return self._balance

    def __str__(self):
        return f"{self.owner}: {self._balance:.2f}"

    def __add__(self, other):
        if isinstance(other, (int, float)):
            self.deposit(other)
            return self
        return NotImplemented

    def __sub__(self, other):
        if isinstance(other, (int, float)):
            self.withdraw(other)
            return self
        return NotImplemented

acc = Account("Alice", 1000)
print(f"开户: {acc}")

acc.deposit(500)
print(f"存款后: {acc}")

acc.withdraw(200)
print(f"取款后: {acc}")

try:
    acc.withdraw(2000)
except BankError as e:
    print(f"取款失败: {e}")

print(f"最终余额: {acc.balance}")

print("\n" + "=" * 50)
print("第五章 完")
print("=" * 50)
```

---

## 知识点速查表

| 类别 | 内容 | 示例 |
|------|------|------|
| 类定义 | class 关键字 | `class Dog:` |
| 对象创建 | 实例化 | `dog = Dog()` |
| 构造方法 | 初始化属性 | `__init__(self, name)` |
| 实例方法 | self 参数 | `def method(self):` |
| 魔方方法 | 运算符重载 | `__str__`, `__add__`, `__eq__` |
| 实例属性 | 每个实例独立 | `self.name = name` |
| 类属性 | 所有实例共享 | `species = "犬科"` |
| @property | getter/setter/deleter | `@property; @x.setter` |
| @classmethod | 类方法、工厂方法 | `@classmethod; def from_str(cls)` |
| @staticmethod | 静态工具方法 | `@staticmethod; def util():` |
| 继承 | 代码复用、super() | `class B(A): super().__init__()` |
| 多态 | 统一接口 | `isinstance(obj, Parent)` |
| 抽象类 | 接口规范 | `class A(ABC): @abstractmethod` |
| 私有约定 | 伪私有属性 | `_x`, `__x` |
| try-except | 异常捕获 | `try: ... except: ...` |
| 自定义异常 | 继承 Exception | `class MyError(Exception):` |
| raise | 抛出异常 | `raise ValueError("msg")` |
| finally | 始终执行 | `finally: ...` |
| with 语句 | 资源管理 | `with open(file) as f:` |
