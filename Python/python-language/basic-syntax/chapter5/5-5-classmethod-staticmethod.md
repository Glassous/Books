# @classmethod 与 @staticmethod

类方法（`@classmethod`）和静态方法（`@staticmethod`）是不依赖实例的方法。

## @classmethod

类方法接收类作为第一个参数（`cls`），可以访问和修改类属性：

```python
class Student:
    school = "第一中学"
    count = 0

    def __init__(self, name):
        self.name = name
        Student.count += 1

    @classmethod
    def get_info(cls):
        return f"{cls.school} - 共 {cls.count} 名学生"

    @classmethod
    def set_school(cls, new_school):
        cls.school = new_school

    @classmethod
    def from_string(cls, text):
        """从字符串创建实例（工厂方法）"""
        name = text.strip().title()
        return cls(name)

# 通过类调用
print(Student.get_info())  # 第一中学 - 共 0 名学生

# 通过实例调用
s1 = Student("alice")
print(s1.get_info())  # 第一中学 - 共 1 名学生

# 修改类属性
Student.set_school("第二中学")
print(Student.get_info())  # 第二中学 - 共 1 名学生

# 工厂方法
s2 = Student.from_string("  bob  ")
print(s2.name)  # Bob
```

## @staticmethod

静态方法不接收类或实例参数，类似于普通函数，但放在类的命名空间中：

```python
class MathUtils:
    @staticmethod
    def is_even(n):
        return n % 2 == 0

    @staticmethod
    def factorial(n):
        result = 1
        for i in range(2, n + 1):
            result *= i
        return result

    @staticmethod
    def is_prime(n):
        if n < 2:
            return False
        for i in range(2, int(n ** 0.5) + 1):
            if n % i == 0:
                return False
        return True

# 通过类调用
print(MathUtils.is_even(10))      # True
print(MathUtils.factorial(5))     # 120
print(MathUtils.is_prime(17))     # True

# 通过实例调用
mu = MathUtils()
print(mu.is_even(7))  # False
```

## 三种方法对比

```python
class Demo:
    def instance_method(self):
        """实例方法：可以访问实例和类"""
        return f"实例: {self}"

    @classmethod
    def class_method(cls):
        """类方法：可以访问类，不能访问实例"""
        return f"类: {cls.__name__}"

    @staticmethod
    def static_method():
        """静态方法：不能访问实例和类"""
        return "静态方法"

d = Demo()
print(d.instance_method())  # 实例: <__main__.Demo object at ...>
print(d.class_method())     # 类: Demo
print(d.static_method())    # 静态方法

# 都可以通过类调用
print(Demo.class_method())    # 类: Demo
print(Demo.static_method())   # 静态方法
# print(Demo.instance_method())  # TypeError
```

## 实际应用

### 配置管理

```python
class Config:
    _settings = {
        "host": "localhost",
        "port": 8080,
        "debug": True
    }

    @classmethod
    def get(cls, key):
        return cls._settings.get(key)

    @classmethod
    def set(cls, key, value):
        cls._settings[key] = value

    @classmethod
    def from_env(cls):
        """从环境变量加载配置"""
        import os
        cls._settings["host"] = os.getenv("HOST", "localhost")
        cls._settings["port"] = int(os.getenv("PORT", 8080))
        return cls

Config.set("debug", False)
print(Config.get("port"))   # 8080
print(Config.get("debug"))  # False
```

### 数据验证

```python
class Validator:
    @staticmethod
    def is_email(text):
        return "@" in text and "." in text.split("@")[-1]

    @staticmethod
    def is_phone(text):
        return len(text) == 11 and text.isdigit()

    @staticmethod
    def is_url(text):
        return text.startswith(("http://", "https://"))

print(Validator.is_email("test@example.com"))  # True
print(Validator.is_phone("13800138000"))       # True
print(Validator.is_url("https://python.org"))  # True
```
