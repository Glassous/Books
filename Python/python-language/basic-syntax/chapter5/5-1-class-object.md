# 类与对象

类（Class）是创建对象的蓝图，对象（Object）是类的实例。面向对象编程将数据和行为封装在一起。

## 定义类

使用 `class` 关键字定义类：

```python
class Dog:
    pass  # 空类
```

## 创建对象

```python
class Dog:
    pass

dog1 = Dog()
dog2 = Dog()

print(dog1)  # <__main__.Dog object at 0x...>
print(dog2)  # <__main__.Dog object at 0x...>
print(type(dog1))  # <class '__main__.Dog'>
```

## __init__ 方法

`__init__` 是构造方法，在创建对象时自动调用，用于初始化属性：

```python
class Dog:
    def __init__(self, name, age):
        self.name = name   # 实例属性
        self.age = age     # 实例属性

dog = Dog("旺财", 3)
print(dog.name)  # 旺财
print(dog.age)   # 3
```

## 类的基本结构

```python
class ClassName:
    """类文档字符串"""

    def __init__(self, 参数列表):
        """构造方法：初始化对象属性"""
        self.属性 = 值

    def 方法名(self, 参数列表):
        """实例方法"""
        pass
```

## 完整示例

```python
class Student:
    """学生类"""

    def __init__(self, name, score):
        self.name = name
        self.score = score

    def introduce(self):
        print(f"我叫{self.name}，成绩{self.score}分")

# 创建对象
s1 = Student("Alice", 95)
s2 = Student("Bob", 82)

# 调用方法
s1.introduce()  # 我叫Alice，成绩95分
s2.introduce()  # 我叫Bob，成绩82分

# 访问属性
print(s1.name)   # Alice
print(s2.score)  # 82
```

## self 参数

`self` 指向实例本身，在实例方法中必须作为第一个参数：

```python
class Cat:
    def __init__(self, name):
        self.name = name

    def meow(self):
        print(f"{self.name}: 喵~")

    def eat(self, food):
        print(f"{self.name} 正在吃 {food}")

cat = Cat("咪咪")
cat.meow()       # 咪咪: 喵~
cat.eat("鱼")    # 咪咪 正在吃 鱼
```

## 类与对象的关系

```python
class Car:
    """汽车类"""
    wheels = 4  # 类属性

    def __init__(self, brand, color):
        self.brand = brand  # 实例属性
        self.color = color

car1 = Car("Toyota", "白色")
car2 = Car("Honda", "黑色")

print(car1.brand)   # Toyota
print(car2.color)   # 黑色
print(car1.wheels)  # 4（共享类属性）
print(Car.wheels)   # 4
```
