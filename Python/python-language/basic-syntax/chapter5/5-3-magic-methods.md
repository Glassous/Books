# 魔方方法

魔方方法（Magic Methods）是 Python 中以双下划线开头和结尾的特殊方法，用于定制类的行为。

## __init__

构造方法，创建对象时自动调用：

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print(f"创建了 {name}")

p = Person("Alice", 25)  # 创建了 Alice
```

## __str__ 与 __repr__

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        """给用户看的字符串表示"""
        return f"{self.name}({self.age}岁)"

    def __repr__(self):
        """给开发者看的字符串表示"""
        return f"Person('{self.name}', {self.age})"

p = Person("Alice", 25)
print(str(p))   # Alice(25岁)
print(repr(p))  # Person('Alice', 25)
```

## __len__

```python
class Team:
    def __init__(self, members):
        self.members = members

    def __len__(self):
        return len(self.members)

team = Team(["Alice", "Bob", "Charlie"])
print(len(team))  # 3
```

## __add__

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = v1 + v2
print(v3)  # Vector(4, 6)
```

## __eq__ 与 __lt__

```python
class Student:
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def __eq__(self, other):
        return self.score == other.score

    def __lt__(self, other):
        return self.score < other.score

    def __str__(self):
        return f"{self.name}: {self.score}"

s1 = Student("Alice", 85)
s2 = Student("Bob", 92)
s3 = Student("Charlie", 85)

print(s1 == s3)  # True
print(s1 < s2)   # True
print(s2 > s1)   # True（自动推导）
```

## __getitem__

```python
class Playlist:
    def __init__(self):
        self.songs = []

    def add(self, song):
        self.songs.append(song)

    def __getitem__(self, index):
        return self.songs[index]

    def __len__(self):
        return len(self.songs)

playlist = Playlist()
playlist.add("稻香")
playlist.add("晴天")
playlist.add("七里香")

print(playlist[0])   # 稻香
print(playlist[1])   # 晴天
print(len(playlist)) # 3

# 支持切片
print(playlist[1:])  # ['晴天', '七里香']
```

## __call__

使实例可以像函数一样调用：

```python
class Counter:
    def __init__(self):
        self.count = 0

    def __call__(self):
        self.count += 1
        return self.count

counter = Counter()
print(counter())  # 1
print(counter())  # 2
print(counter())  # 3
```

## 常见魔方方法汇总

```python
class Demo:
    def __init__(self):       # 构造方法
        pass
    def __str__(self):        # 字符串表示（用户）
        return "Demo"
    def __repr__(self):       # 字符串表示（开发者）
        return "Demo()"
    def __len__(self):        # len() 函数
        return 0
    def __add__(self, other): # + 运算符
        return self
    def __eq__(self, other):  # == 比较
        return True
    def __lt__(self, other):  # < 比较
        return True
    def __getitem__(self, k): # 索引访问 obj[k]
        return k
    def __setitem__(self, k, v):  # 索引赋值 obj[k] = v
        pass
    def __call__(self):       # 调用实例 obj()
        pass
    def __contains__(self, item):  # in 运算符
        return True
    def __bool__(self):       # bool() 转换
        return True
    def __iter__(self):       # 迭代器
        return iter([])
```
