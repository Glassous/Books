# 列表案例

## 案例一：学生成绩管理系统

```python
# 学生成绩管理
scores = [85, 92, 78, 95, 88, 76, 90, 82]

# 统计
total = sum(scores)
average = total / len(scores)
max_score = max(scores)
min_score = min(scores)

print(f"成绩列表: {scores}")
print(f"总分: {total}")
print(f"平均分: {average:.1f}")
print(f"最高分: {max_score}")
print(f"最低分: {min_score}")

# 筛选及格和优秀
passing = [s for s in scores if s >= 60]
excellent = [s for s in scores if s >= 90]
print(f"及格人数: {len(passing)}")
print(f"优秀人数: {len(excellent)}")

# 排序
scores.sort(reverse=True)
print(f"排名: {scores}")

# 分段统计
def grade_stats(scores):
    levels = {"优秀(90-100)": 0, "良好(80-89)": 0,
              "中等(70-79)": 0, "及格(60-69)": 0, "不及格(<60)": 0}
    for s in scores:
        if s >= 90: levels["优秀(90-100)"] += 1
        elif s >= 80: levels["良好(80-89)"] += 1
        elif s >= 70: levels["中等(70-79)"] += 1
        elif s >= 60: levels["及格(60-69)"] += 1
        else: levels["不及格(<60)"] += 1
    return levels

for level, count in grade_stats(scores).items():
    print(f"{level}: {count}人")
```

## 案例二：任务队列

```python
class TaskQueue:
    def __init__(self):
        self.tasks = []

    def add_task(self, task, priority=0):
        self.tasks.append({"task": task, "priority": priority})
        self.tasks.sort(key=lambda x: x["priority"], reverse=True)

    def execute_next(self):
        if not self.tasks:
            return "没有任务"
        task = self.tasks.pop(0)
        return f"执行: {task['task']}"

    def show_queue(self):
        return [t["task"] for t in self.tasks]

    def clear(self):
        self.tasks.clear()

queue = TaskQueue()
queue.add_task("写报告", 2)
queue.add_task("发邮件", 1)
queue.add_task("紧急修复", 5)
queue.add_task("整理文件", 0)

print(f"任务队列: {queue.show_queue()}")
print(queue.execute_next())
print(f"剩余任务: {queue.show_queue()}")
```

## 案例三：矩阵操作

```python
# 矩阵转置
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

transposed = [[row[i] for row in matrix] for i in range(3)]
print("原矩阵:")
for row in matrix:
    print(row)
print("转置后:")
for row in transposed:
    print(row)

# 矩阵乘法
def matrix_multiply(A, B):
    result = [[0] * len(B[0]) for _ in range(len(A))]
    for i in range(len(A)):
        for j in range(len(B[0])):
            for k in range(len(B)):
                result[i][j] += A[i][k] * B[k][j]
    return result

A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]
C = matrix_multiply(A, B)
print(f"A x B = {C}")

# 矩阵旋转
def rotate_matrix(matrix):
    n = len(matrix)
    result = [[0] * n for _ in range(n)]
    for i in range(n):
        for j in range(n):
            result[j][n - 1 - i] = matrix[i][j]
    return result

rotated = rotate_matrix(matrix)
print("旋转90度:")
for row in rotated:
    print(row)
```

## 案例四：数据去重与统计

```python
data = [1, 3, 2, 3, 4, 2, 1, 5, 3, 4, 1, 2]

# 去重（保持顺序）
seen = set()
unique = []
for item in data:
    if item not in seen:
        unique.append(item)
        seen.add(item)
print(f"原数据: {data}")
print(f"去重后: {unique}")

# 频率统计
freq = {}
for item in data:
    freq[item] = freq.get(item, 0) + 1
print(f"频率: {freq}")

# 按频率排序
sorted_by_freq = sorted(freq.items(), key=lambda x: x[1], reverse=True)
print(f"按频率排序: {sorted_by_freq}")

# 找出出现次数最多的元素
max_count = max(freq.values())
most_common = [k for k, v in freq.items() if v == max_count]
print(f"出现最多的元素: {most_common}")
```

## 案例五：排序算法实现

```python
# 冒泡排序
def bubble_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        swapped = False
        for j in range(n - 1 - i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr

# 选择排序
def selection_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr

# 快速排序
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[0]
    left = [x for x in arr[1:] if x <= pivot]
    right = [x for x in arr[1:] if x > pivot]
    return quick_sort(left) + [pivot] + quick_sort(right)

test = [64, 34, 25, 12, 22, 11, 90]
print(f"冒泡排序: {bubble_sort(test.copy())}")
print(f"选择排序: {selection_sort(test.copy())}")
print(f"快速排序: {quick_sort(test.copy())}")
```

## 案例六：滑动窗口

```python
def max_sliding_window(nums, k):
    if not nums:
        return []
    result = []
    for i in range(len(nums) - k + 1):
        window = nums[i:i + k]
        result.append(max(window))
    return result

def sliding_average(nums, k):
    result = []
    window_sum = sum(nums[:k])
    result.append(window_sum / k)
    for i in range(k, len(nums)):
        window_sum += nums[i] - nums[i - k]
        result.append(window_sum / k)
    return result

nums = [1, 3, -1, -3, 5, 3, 6, 7]
print(f"滑动窗口最大值: {max_sliding_window(nums, 3)}")
print(f"滑动窗口平均值: {sliding_average(nums, 3)}")
```
