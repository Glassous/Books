# 实例属性与类属性

Python 的属性分为实例属性（Instance Attribute）和类属性（Class Attribute）。

## 实例属性

每个实例独立拥有，在 `__init__` 或其他方法中通过 `self` 定义：

```python
class Student:
    def __init__(self, name, score):
        self.name = name      # 实例属性
        self.score = score    # 实例属性

s1 = Student("Alice", 95)
s2 = Student("Bob", 82)

print(s1.name)   # Alice
print(s2.name)   # Bob（各自独立）
```

## 类属性

所有实例共享，直接在类中定义：

```python
class Student:
    school = "第一中学"  # 类属性

    def __init__(self, name, score):
        self.name = name
        self.score = score

s1 = Student("Alice", 95)
s2 = Student("Bob", 82)

print(s1.school)  # 第一中学
print(s2.school)  # 第一中学（共享）
print(Student.school)  # 第一中学（通过类访问）
```

## 属性查找顺序

实例属性优先于类属性：

```python
class Student:
    school = "第一中学"

    def __init__(self, name):
        self.name = name

s = Student("Alice")
print(s.school)  # 第一中学（从类查找）

# 动态添加实例属性，覆盖类属性
s.school = "第二中学"
print(s.school)        # 第二中学（实例属性优先）
print(Student.school)  # 第一中学（类属性不变）

# 删除实例属性后恢复为类属性
del s.school
print(s.school)  # 第一中学
```

## 类属性的用途

### 计数器

```python
class User:
    count = 0  # 类属性：计数

    def __init__(self, name):
        self.name = name
        User.count += 1  # 每次创建实例 count +1

u1 = User("Alice")
u2 = User("Bob")
u3 = User("Charlie")

print(User.count)  # 3
```

### 常量定义

```python
class Math:
    PI = 3.14159
    E = 2.71828
    GOLDEN_RATIO = 1.618

print(Math.PI)  # 3.14159
```

### 配置参数

```python
class Database:
    host = "localhost"
    port = 3306
    user = "admin"
    password = "123456"

    @classmethod
    def get_config(cls):
        return f"{cls.user}@{cls.host}:{cls.port}"

print(Database.get_config())  # admin@localhost:3306
```

## 动态添加属性

```python
class Person:
    def __init__(self, name):
        self.name = name

p = Person("Alice")

# 动态添加实例属性
p.age = 25
p.city = "Beijing"
print(p.age)   # 25
print(p.city)  # Beijing

# 动态添加类属性
Person.species = "Human"
print(p.species)   # Human
```

## @property 装饰器

将方法转换为属性访问：

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius

    @property
    def celsius(self):
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("温度不能低于绝对零度")
        self._celsius = value

    @property
    def fahrenheit(self):
        return self._celsius * 9 / 5 + 32

temp = Temperature(25)
print(temp.celsius)     # 25（像属性一样访问）
print(temp.fahrenheit)  # 77.0

temp.celsius = 30
print(temp.fahrenheit)  # 86.0

# temp.celsius = -300  # ValueError
```

## 私有属性约定

以单下划线 `_` 开头表示保护属性，双下划线 `__` 开头触发名称修饰：

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self._balance = balance       # 保护属性（约定）
        self.__password = "123456"    # 名称修饰（伪私有）

    def get_balance(self):
        return self._balance

account = BankAccount("Alice", 1000)
print(account.owner)       # Alice
print(account._balance)    # 1000（可以访问，但不推荐）
# print(account.__password)  # AttributeError
print(account._BankAccount__password)  # 123456（名称修饰后的真实名称）
```
