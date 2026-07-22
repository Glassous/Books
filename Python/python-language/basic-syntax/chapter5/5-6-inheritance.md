# 继承与多态

继承（Inheritance）允许一个类从另一个类获取属性和方法，实现代码复用。多态（Polymorphism）允许不同类的对象通过统一接口调用。

## 基本继承

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "..."
        
    def move(self):
        return "移动中"

class Dog(Animal):
    def speak(self):
        return "汪汪！"

class Cat(Animal):
    def speak(self):
        return "喵~"

dog = Dog("旺财")
cat = Cat("咪咪")

print(f"{dog.name}: {dog.speak()}")  # 旺财: 汪汪！
print(f"{cat.name}: {cat.speak()}")  # 咪咪: 喵~
print(dog.move())  # 移动中（继承自 Animal）
```

## super()

调用父类的方法：

```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)  # 调用父类的 __init__
        self.breed = breed

    def __str__(self):
        return f"{self.breed}犬 {self.name}"

dog = Dog("旺财", "金毛")
print(dog)  # 金毛犬 旺财
```

## 方法重写

子类可以完全替换或扩展父类方法：

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand

    def start(self):
        return "启动引擎"

    def info(self):
        return f"{self.brand} 车辆"

class ElectricCar(Vehicle):
    def start(self):
        return "接通电源"  # 完全重写

    def info(self):
        parent_info = super().info()  # 扩展
        return f"{parent_info}（电动车）"

tesla = ElectricCar("Tesla")
print(tesla.start())  # 接通电源
print(tesla.info())   # Tesla 车辆（电动车）
```

## 多态

不同类的对象响应相同的接口：

```python
class Bird:
    def speak(self):
        return "叽叽喳喳"

class Duck(Bird):
    def speak(self):
        return "嘎嘎"

class Chicken(Bird):
    def speak(self):
        return "咯咯哒"

def animal_sound(animal):
    """多态：统一接口调用"""
    print(animal.speak())

animals = [Bird(), Duck(), Chicken(), Dog("狗"), Cat("猫")]
for a in animals:
    animal_sound(a)
```

## 类型检查

```python
class Animal: pass
class Dog(Animal): pass
class Cat(Animal): pass

dog = Dog()
cat = Cat()

print(isinstance(dog, Dog))     # True
print(isinstance(dog, Animal))  # True（Dog 是 Animal 的子类）
print(issubclass(Dog, Animal))  # True
print(issubclass(Animal, Dog))  # False
```

## 多继承

```python
class Flyable:
    def fly(self):
        return "飞行中"

class Swimmable:
    def swim(self):
        return "游泳中"

class Duck(Flyable, Swimmable):
    def __init__(self, name):
        self.name = name

duck = Duck("唐老鸭")
print(duck.fly())   # 飞行中
print(duck.swim())  # 游泳中

# MRO（方法解析顺序）
print(Duck.__mro__)
# Duck -> Flyable -> Swimmable -> object
```

## 抽象基类

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    """抽象基类：不能直接实例化"""

    @abstractmethod
    def area(self):
        """计算面积（子类必须实现）"""
        pass

    @abstractmethod
    def perimeter(self):
        """计算周长（子类必须实现）"""
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14159 * self.radius ** 2

    def perimeter(self):
        return 2 * 3.14159 * self.radius

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

# shape = Shape()  # TypeError: Can't instantiate abstract class

shapes = [Circle(5), Rectangle(3, 4)]
for s in shapes:
    print(f"面积: {s.area():.2f}, 周长: {s.perimeter():.2f}")
```

## isinstance 与多态实践

```python
class LogWriter:
    def write(self, message):
        pass

class FileLogger(LogWriter):
    def write(self, message):
        return f"写入文件: {message}"

class ConsoleLogger(LogWriter):
    def write(self, message):
        return f"控制台输出: {message}"

class DatabaseLogger(LogWriter):
    def write(self, message):
        return f"写入数据库: {message}"

def log_message(logger, message):
    if not isinstance(logger, LogWriter):
        raise TypeError("需要 LogWriter 实例")
    print(logger.write(message))

log_message(FileLogger(), "系统启动")
log_message(ConsoleLogger(), "用户登录")
log_message(DatabaseLogger(), "数据更新")
```
