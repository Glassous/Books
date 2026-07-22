# 函数类型注解

类型注解（Type Hints）是 Python 3.5+ 引入的可选语法，用于提示参数和返回值的预期类型。

## 基本语法

```python
def add(a: int, b: int) -> int:
    return a + b

def greet(name: str) -> str:
    return f"Hello, {name}"

def show(message: str) -> None:
    print(message)
```

## 变量注解

```python
name: str = "Alice"
age: int = 25
is_active: bool = True
scores: list = [85, 92, 78]
```

## 容器类型注解

使用 `typing` 模块描述容器内元素的类型：

```python
from typing import List, Tuple, Dict, Set, Optional

# 列表
def process_numbers(numbers: List[int]) -> int:
    return sum(numbers)

# 元组
def get_user() -> Tuple[str, int]:
    return ("Alice", 25)

# 字典
def lookup(data: Dict[str, int], key: str) -> Optional[int]:
    return data.get(key)

# 集合
def unique_values(values: Set[int]) -> List[int]:
    return sorted(values)

print(process_numbers([1, 2, 3, 4, 5]))       # 15
print(get_user())                               # ('Alice', 25)
print(lookup({"a": 1, "b": 2}, "a"))           # 1
print(lookup({"a": 1, "b": 2}, "c"))           # None
print(unique_values({3, 1, 2, 1, 3}))          # [1, 2, 3]
```

## Optional 类型

表示参数可以是指定类型或 `None`：

```python
from typing import Optional

def find_user(user_id: int) -> Optional[str]:
    users = {1: "Alice", 2: "Bob"}
    return users.get(user_id)

# 参数可选
def greet(name: Optional[str] = None) -> str:
    if name is None:
        return "Hello, stranger!"
    return f"Hello, {name}!"

print(find_user(1))       # Alice
print(find_user(3))       # None
print(greet())            # Hello, stranger!
print(greet("Charlie"))   # Hello, Charlie!
```

## Union 类型

参数或返回值可以是多种类型之一：

```python
from typing import Union

def to_number(value: Union[str, int, float]) -> Union[int, float]:
    if isinstance(value, str):
        return int(value)
    return value

def process(value: Union[int, float, str]) -> str:
    if isinstance(value, (int, float)):
        return f"数字: {value}"
    return f"字符串: {value}"

print(to_number("42"))    # 42
print(to_number(3.14))    # 3.14
print(process(100))       # 数字: 100
print(process("hello"))   # 字符串: hello
```

## 类型别名

为复杂类型定义简短的别名：

```python
from typing import List, Tuple

# 定义别名
Point = Tuple[float, float]
Polygon = List[Point]

def calculate_area(polygon: Polygon) -> float:
    """计算多边形面积（简化的三角剖分）"""
    if len(polygon) < 3:
        return 0.0
    area = 0.0
    for i in range(len(polygon)):
        x1, y1 = polygon[i]
        x2, y2 = polygon[(i + 1) % len(polygon)]
        area += x1 * y2 - x2 * y1
    return abs(area) / 2

triangle: Polygon = [(0.0, 0.0), (1.0, 0.0), (0.0, 1.0)]
print(calculate_area(triangle))  # 0.5
```

## 函数作为参数的类型

```python
from typing import Callable

# Callable[[参数类型], 返回值类型]
def apply(func: Callable[[int], int], value: int) -> int:
    return func(value)

def double(x: int) -> int:
    return x * 2

def square(x: int) -> int:
    return x * x

print(apply(double, 5))   # 10
print(apply(square, 5))   # 25

# 多参数的函数类型
def operate(a: int, b: int, op: Callable[[int, int], int]) -> int:
    return op(a, b)

print(operate(10, 5, lambda x, y: x + y))  # 15
print(operate(10, 5, lambda x, y: x * y))  # 50
```

## Any 类型

表示任意类型（关闭类型检查）：

```python
from typing import Any

def log(message: Any) -> None:
    print(f"[LOG] {message}")

log("hello")
log(42)
log([1, 2, 3])
```

## 实际应用示例

```python
from typing import List, Dict, Optional, Callable

# 学生成绩管理
Student = Dict[str, any]
GradeCalculator = Callable[[int], str]

def calculate_grade(score: int) -> str:
    if score >= 90: return "优秀"
    if score >= 80: return "良好"
    if score >= 70: return "中等"
    if score >= 60: return "及格"
    return "不及格"

def process_scores(
    scores: List[int],
    grade_func: GradeCalculator = calculate_grade
) -> List[Student]:
    students: List[Student] = []
    for i, score in enumerate(scores, 1):
        students.append({
            "id": i,
            "score": score,
            "grade": grade_func(score)
        })
    return students

def find_top_student(
    students: List[Student]
) -> Optional[Student]:
    if not students:
        return None
    return max(students, key=lambda s: s["score"])

scores = [85, 92, 73, 58, 90]
students = process_scores(scores)
top = find_top_student(students)

print(f"最高分学生: {top}")
for s in students:
    print(f"  学生{s['id']}: {s['score']}分 -> {s['grade']}")
```
