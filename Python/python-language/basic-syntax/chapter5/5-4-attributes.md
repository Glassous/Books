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

`@property` 将方法转换为属性访问，实现对属性的精细控制。

### getter 与 setter

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius

    @property
    def celsius(self):
        """getter：像属性一样读取"""
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        """setter：赋值时进行验证"""
        if value < -273.15:
            raise ValueError("温度不能低于绝对零度")
        self._celsius = value

    @celsius.deleter
    def celsius(self):
        """deleter：删除时处理"""
        print("删除温度数据")
        del self._celsius

temp = Temperature(25)
print(temp.celsius)      # 25（调用 getter）
temp.celsius = 30        # 调用 setter
# temp.celsius = -300    # ValueError
# del temp.celsius       # 删除温度数据
```

### 计算属性

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    @property
    def area(self):
        """面积（只读，每次实时计算）"""
        return self.width * self.height

    @property
    def perimeter(self):
        """周长"""
        return 2 * (self.width + self.height)

r = Rectangle(3, 4)
print(r.area)       # 12（像属性一样访问）
print(r.perimeter)  # 14
r.width = 5
print(r.area)       # 20（自动更新）
```

### 缓存属性

```python
class DataProcessor:
    def __init__(self, data):
        self._data = data
        self._cached_result = None

    @property
    def data(self):
        return self._data

    @data.setter
    def data(self, value):
        self._data = value
        self._cached_result = None  # 数据变化时清除缓存

    @property
    def result(self):
        if self._cached_result is None:
            print("计算中...")
            self._cached_result = sum(x ** 2 for x in self._data)
        return self._cached_result

dp = DataProcessor([1, 2, 3, 4, 5])
print(dp.result)  # 计算中... 55
print(dp.result)  # 55（命中缓存）

dp.data = [2, 3, 4]
print(dp.result)  # 计算中... 29（缓存已清除）
```

### 数据验证

```python
class User:
    def __init__(self, name, age):
        self.name = name
        self._age = 0
        self.age = age  # 通过 setter 赋值

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if not isinstance(value, int):
            raise TypeError("年龄必须是整数")
        if not 0 <= value <= 150:
            raise ValueError("年龄必须在 0-150 之间")
        self._age = value

    @property
    def is_adult(self):
        return self._age >= 18

u = User("Alice", 25)
print(u.age)       # 25
print(u.is_adult)  # True
# u.age = -5       # ValueError
# u.age = "abc"    # TypeError
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
