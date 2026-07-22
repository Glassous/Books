# 元组案例

## 案例一：坐标与几何计算

```python
import math

# 计算两点距离
def distance(p1, p2):
    return math.sqrt((p1[0] - p2[0])**2 + (p1[1] - p2[1])**2)

# 计算多边形周长
def polygon_perimeter(*points):
    perimeter = 0
    n = len(points)
    for i in range(n):
        p1 = points[i]
        p2 = points[(i + 1) % n]
        perimeter += distance(p1, p2)
    return perimeter

# 计算多边形面积（鞋带公式）
def polygon_area(*points):
    area = 0
    n = len(points)
    for i in range(n):
        x1, y1 = points[i]
        x2, y2 = points[(i + 1) % n]
        area += x1 * y2 - x2 * y1
    return abs(area) / 2

# 测试
triangle = ((0, 0), (3, 0), (0, 4))
print(f"三角形周长: {polygon_perimeter(*triangle)}")
print(f"三角形面积: {polygon_area(*triangle)}")

square = ((0, 0), (4, 0), (4, 4), (0, 4))
print(f"正方形周长: {polygon_perimeter(*square)}")
print(f"正方形面积: {polygon_area(*square)}")

# 点的最近邻
def nearest_neighbor(target, points):
    nearest = None
    min_dist = float("inf")
    for point in points:
        dist = distance(target, point)
        if dist < min_dist:
            min_dist = dist
            nearest = point
    return nearest, min_dist

target = (5, 5)
points = [(1, 2), (4, 6), (8, 3), (2, 8)]
nearest, dist = nearest_neighbor(target, points)
print(f"最近点: {nearest}, 距离: {dist:.2f}")
```

## 案例二：学生信息管理

```python
# 使用元组表示学生记录（name, age, grade, subjects）
students = [
    ("Alice", 20, 85, ("Math", "Physics", "CS")),
    ("Bob", 22, 92, ("Math", "Chemistry", "Biology")),
    ("Charlie", 21, 78, ("History", "Literature", "Art")),
    ("Diana", 20, 95, ("Math", "CS", "Physics")),
]

# 按成绩排序
by_grade = sorted(students, key=lambda s: s[2], reverse=True)
print("成绩排名:")
for name, age, grade, subjects in by_grade:
    print(f"  {name}: {grade}")

# 查找共同科目
def common_subjects(s1, s2):
    subs1 = set(s1[3])
    subs2 = set(s2[3])
    return subs1 & subs2

print(f"\n共同科目: {common_subjects(students[0], students[3])}")

# 按专业筛选
cs_students = [s for s in students if "CS" in s[3]]
print(f"学CS的学生: {[s[0] for s in cs_students]}")

# 统计信息
grades = [s[2] for s in students]
print(f"\n平均分: {sum(grades)/len(grades):.1f}")
print(f"最高分: {max(grades)}")
print(f"最低分: {min(grades)}")

# 元组作为字典键（复合键）
grade_book = {}
for name, age, grade, subjects in students:
    for subject in subjects:
        key = (subject, name)
        grade_book[key] = grade

print(f"\nAlice的数学成绩: {grade_book.get(('Math', 'Alice'))}")
```

## 案例三：数据点聚类（简化版）

```python
import random
import math

def generate_points(n, max_coord=100):
    points = []
    for _ in range(n):
        x = random.randint(0, max_coord)
        y = random.randint(0, max_coord)
        points.append((x, y))
    return tuple(points)

def euclidean_dist(p1, p2):
    return math.sqrt((p1[0]-p2[0])**2 + (p1[1]-p2[1])**2)

def k_means_clustering(points, k=3, max_iter=100):
    centroids = list(points[:k])

    for _ in range(max_iter):
        clusters = [[] for _ in range(k)]
        for p in points:
            distances = [euclidean_dist(p, c) for c in centroids]
            cluster_idx = distances.index(min(distances))
            clusters[cluster_idx].append(p)

        new_centroids = []
        for cluster in clusters:
            if cluster:
                avg_x = sum(p[0] for p in cluster) / len(cluster)
                avg_y = sum(p[1] for p in cluster) / len(cluster)
                new_centroids.append((avg_x, avg_y))
            else:
                new_centroids.append(random.choice(points))

        if new_centroids == centroids:
            break
        centroids = new_centroids

    return centroids, clusters

points = generate_points(20, 50)
centroids, clusters = k_means_clustering(points, k=3)

print("聚类中心:")
for i, c in enumerate(centroids):
    print(f"  簇{i}: ({c[0]:.1f}, {c[1]:.1f}), {len(clusters[i])}个点")
```

## 案例四：不可变配置管理

```python
# 使用元组表示不可变配置
class AppConfig:
    DEFAULTS = (
        ("database", ("localhost", 5432, "app_db", "user", "pass")),
        ("redis", ("localhost", 6379, 0)),
        ("logging", ("INFO", "app.log", 10485760, 5)),
        ("cache", ("memory", 300, 1000)),
    )

    @classmethod
    def get_config(cls, section):
        for key, value in cls.DEFAULTS:
            if key == section:
                return value
        return None

    @classmethod
    def show_all(cls):
        for key, value in cls.DEFAULTS:
            print(f"\n[{key}]")
            for i, v in enumerate(value):
                print(f"  {i}: {v}")

print("默认配置:")
AppConfig.show_all()

db_config = AppConfig.get_config("database")
host, port, name, user, password = db_config
print(f"\n数据库连接: {user}@{host}:{port}/{name}")
```

## 案例五：函数多返回值

```python
def analyze_numbers(*numbers):
    return (
        min(numbers),
        max(numbers),
        sum(numbers) / len(numbers),
        sum(numbers),
        len(numbers)
    )

def fibonacci_sequence(n):
    a, b = 0, 1
    sequence = []
    for _ in range(n):
        sequence.append(a)
        a, b = b, a + b
    return tuple(sequence)

def divide_and_remainder(a, b):
    return (a // b, a % b)

# 测试
numbers = [85, 92, 78, 95, 88]
minimum, maximum, average, total, count = analyze_numbers(*numbers)
print(f"最小值: {minimum}")
print(f"最大值: {maximum}")
print(f"平均值: {average:.1f}")
print(f"总和: {total}")
print(f"数量: {count}")

fib = fibonacci_sequence(10)
print(f"斐波那契: {fib}")

quotient, remainder = divide_and_remainder(17, 5)
print(f"17 ÷ 5 = {quotient} 余 {remainder}")
```
