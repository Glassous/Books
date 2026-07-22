# 字典案例

## 案例一：学生成绩管理系统

```python
class GradeBook:
    def __init__(self):
        self.students = {}

    def add_student(self, name):
        if name not in self.students:
            self.students[name] = {}

    def add_grade(self, name, subject, score):
        self.add_student(name)
        self.students[name][subject] = score

    def get_average(self, name):
        scores = self.students.get(name, {}).values()
        return sum(scores) / len(scores) if scores else 0

    def get_rankings(self):
        averages = {name: self.get_average(name) for name in self.students}
        return sorted(averages.items(), key=lambda x: x[1], reverse=True)

    def subject_stats(self, subject):
        subject_grades = {}
        for name, grades in self.students.items():
            if subject in grades:
                subject_grades[name] = grades[subject]

        if not subject_grades:
            return None

        scores = list(subject_grades.values())
        return {
            "平均分": sum(scores) / len(scores),
            "最高分": max(scores),
            "最低分": min(scores),
            "人数": len(scores)
        }

    def report(self):
        for name, grades in sorted(self.students.items()):
            avg = self.get_average(name)
            print(f"{name}: 平均分 {avg:.1f}")
            for subject, score in sorted(grades.items()):
                print(f"  {subject}: {score}")

gb = GradeBook()
data = [
    ("Alice", "Math", 95), ("Alice", "Physics", 88),
    ("Bob", "Math", 78), ("Bob", "Physics", 82), ("Bob", "CS", 91),
    ("Charlie", "Math", 92), ("Charlie", "CS", 96),
]

for name, subject, score in data:
    gb.add_grade(name, subject, score)

print("成绩报告:")
gb.report()
print(f"\n排名: {gb.get_rankings()}")
print(f"\n数学统计: {gb.subject_stats('Math')}")
```

## 案例二：JSON 数据处理

```python
import json

# 模拟从 API 获取的数据
data_str = """
{
    "users": [
        {"id": 1, "name": "Alice", "email": "alice@example.com", "age": 25, "active": true},
        {"id": 2, "name": "Bob", "email": "bob@example.com", "age": 30, "active": false},
        {"id": 3, "name": "Charlie", "email": "charlie@example.com", "age": 35, "active": true}
    ],
    "total": 3,
    "page": 1
}
"""

data = json.loads(data_str)

# 数据分析
users = data["users"]
active_users = [u for u in users if u["active"]]
ages = [u["age"] for u in users]

print(f"总用户数: {len(users)}")
print(f"活跃用户: {len(active_users)}")
print(f"平均年龄: {sum(ages)/len(ages):.1f}")

# 构建索引
user_by_id = {u["id"]: u for u in users}
user_by_email = {u["email"]: u for u in users}

print(f"ID 1: {user_by_id[1]['name']}")
print(f"bob@example.com: {user_by_email['bob@example.com']['name']}")

# 分组统计
from collections import Counter
age_groups = Counter()
for u in users:
    if u["age"] < 30:
        age_groups["20-29"] += 1
    elif u["age"] < 40:
        age_groups["30-39"] += 1
    else:
        age_groups["40+"] += 1

print(f"年龄分组: {dict(age_groups)}")

# 导出 CSV
csv_lines = ["name,email,age,active"]
for u in users:
    csv_lines.append(f"{u['name']},{u['email']},{u['age']},{u['active']}")
print("\nCSV:")
print("\n".join(csv_lines))
```

## 案例三：缓存系统

```python
import time
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity=100):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key):
        if key not in self.cache:
            return None
        self.cache.move_to_end(key)
        return self.cache[key]

    def put(self, key, value):
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)

    def __contains__(self, key):
        return key in self.cache

    def stats(self):
        return {
            "size": len(self.cache),
            "capacity": self.capacity,
            "keys": list(self.cache.keys())
        }

cache = LRUCache(3)
cache.put("a", 1)
cache.put("b", 2)
cache.put("c", 3)
print(f"缓存: {cache.stats()}")

cache.get("a")
cache.put("d", 4)
print(f"访问a后添加d: {cache.stats()}")  # b 被淘汰

cache.put("e", 5)
print(f"添加e后: {cache.stats()}")  # c 被淘汰
```

## 案例四：词频统计

```python
def word_frequency(text):
    # 清洗文本
    import re
    words = re.findall(r'\b\w+\b', text.lower())
    stop_words = {"the", "a", "an", "in", "on", "at", "to",
                  "for", "of", "and", "is", "are", "it"}

    freq = {}
    for word in words:
        if word not in stop_words:
            freq[word] = freq.get(word, 0) + 1

    return freq

def top_n_words(freq, n=10):
    return sorted(freq.items(), key=lambda x: x[1], reverse=True)[:n]

def word_cloud_data(text):
    freq = word_frequency(text)
    return [{"word": word, "count": count, "size": count * 10}
            for word, count in top_n_words(freq, 20)]

text = """
Python is a powerful programming language. Python is easy to learn and 
fun to use. Many developers love Python because Python is versatile.
Python can be used for web development, data science, and automation.
Learning Python opens many doors in software development.
"""

freq = word_frequency(text)
print("词频统计:")
for word, count in top_n_words(freq, 5):
    print(f"  {word}: {count}")

print("\n词云数据:")
for item in word_cloud_data(text)[:5]:
    print(f"  {item}")
```

## 案例五：电话号码簿

```python
class PhoneBook:
    def __init__(self):
        self.contacts = {}

    def add(self, name, phone, email=None, group=None):
        self.contacts[name] = {
            "phone": phone,
            "email": email,
            "group": group or "default"
        }

    def search(self, query):
        results = {}
        for name, info in self.contacts.items():
            if query.lower() in name.lower() or query in info["phone"]:
                results[name] = info
        return results

    def get_group(self, group_name):
        return {n: i for n, i in self.contacts.items()
                if i["group"] == group_name}

    def export_vcard(self, name):
        if name not in self.contacts:
            return ""
        info = self.contacts[name]
        return f"""BEGIN:VCARD
VERSION:3.0
FN:{name}
TEL:{info['phone']}
EMAIL:{info.get('email', '')}
END:VCARD"""

pb = PhoneBook()
pb.add("Alice", "13800138001", "alice@example.com", "family")
pb.add("Bob", "13900139002", "bob@example.com", "work")
pb.add("Charlie", "13700137003", group="work")

print("搜索 'alice':")
for name, info in pb.search("alice").items():
    print(f"  {name}: {info['phone']}")

print("\n工作群组:")
for name in pb.get_group("work"):
    print(f"  {name}")

print("\nvCard:")
print(pb.export_vcard("Alice"))
```

## 案例六：图论基础

```python
class Graph:
    def __init__(self):
        self.adjacency = {}

    def add_edge(self, u, v):
        self.adjacency.setdefault(u, set()).add(v)
        self.adjacency.setdefault(v, set()).add(u)

    def bfs(self, start):
        visited = set()
        queue = [start]
        result = []

        while queue:
            node = queue.pop(0)
            if node not in visited:
                visited.add(node)
                result.append(node)
                queue.extend(self.adjacency.get(node, set()) - visited)
        return result

    def dfs(self, start):
        visited = set()
        result = []

        def _dfs(node):
            if node not in visited:
                visited.add(node)
                result.append(node)
                for neighbor in self.adjacency.get(node, set()):
                    _dfs(neighbor)

        _dfs(start)
        return result

    def shortest_path(self, start, end):
        if start not in self.adjacency:
            return None

        queue = [[start]]
        visited = {start}

        while queue:
            path = queue.pop(0)
            node = path[-1]
            if node == end:
                return path
            for neighbor in self.adjacency.get(node, set()):
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(path + [neighbor])
        return None

g = Graph()
edges = [(1, 2), (1, 3), (2, 4), (3, 4), (4, 5)]
for u, v in edges:
    g.add_edge(u, v)

print(f"从1开始BFS: {g.bfs(1)}")
print(f"从1开始DFS: {g.dfs(1)}")
print(f"1到5的最短路径: {g.shortest_path(1, 5)}")
```
