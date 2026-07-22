# 列表用法详解

## 索引操作

### 正向索引

```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]

print(fruits[0])   # apple
print(fruits[2])   # cherry
print(fruits[4])   # elderberry
```

### 反向索引

```python
print(fruits[-1])  # elderberry
print(fruits[-3])  # cherry
```

### 切片

```python
print(fruits[1:4])     # ['banana', 'cherry', 'date']
print(fruits[:3])      # ['apple', 'banana', 'cherry']
print(fruits[2:])      # ['cherry', 'date', 'elderberry']
print(fruits[::2])     # ['apple', 'cherry', 'elderberry']
print(fruits[::-1])    # 反转
```

## 添加元素

```python
fruits = ["apple"]

# append() - 末尾添加
fruits.append("banana")
print(fruits)  # ['apple', 'banana']

# insert() - 指定位置插入
fruits.insert(0, "avocado")
print(fruits)  # ['avocado', 'apple', 'banana']

# extend() - 扩展列表
fruits.extend(["cherry", "date"])
print(fruits)  # ['avocado', 'apple', 'banana', 'cherry', 'date']

# += 运算符
fruits += ["elderberry"]
print(fruits)  # ['avocado', 'apple', 'banana', 'cherry', 'date', 'elderberry']
```

## 删除元素

```python
fruits = ["apple", "banana", "cherry", "date", "banana"]

# remove() - 删除指定值（第一个匹配）
fruits.remove("banana")
print(fruits)  # ['apple', 'cherry', 'date', 'banana']

# pop() - 删除并返回指定索引
last = fruits.pop()
print(last)    # banana
print(fruits)  # ['apple', 'cherry', 'date']

# pop(i) - 删除并返回指定索引
second = fruits.pop(1)
print(second)  # cherry
print(fruits)  # ['apple', 'date']

# del 语句
del fruits[0]
print(fruits)  # ['date']

# clear() - 清空列表
fruits.clear()
print(fruits)  # []

# 切片赋值删除
nums = [1, 2, 3, 4, 5]
nums[1:3] = []
print(nums)  # [1, 4, 5]
```

## 修改元素

```python
numbers = [1, 2, 3, 4, 5]

# 修改单个元素
numbers[0] = 10
print(numbers)  # [10, 2, 3, 4, 5]

# 切片修改
numbers[1:3] = [20, 30]
print(numbers)  # [10, 20, 30, 4, 5]

# 切片扩展
numbers[3:] = [40, 50, 60]
print(numbers)  # [10, 20, 30, 40, 50, 60]
```

## 查找元素

```python
fruits = ["apple", "banana", "cherry", "banana"]

# index() - 查找索引
print(fruits.index("banana"))     # 1
print(fruits.index("banana", 2))  # 3（从索引2开始查找）

# count() - 统计出现次数
print(fruits.count("banana"))  # 2

# in 运算符
print("apple" in fruits)   # True
print("grape" in fruits)   # False
```

## 排序操作

```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

# sort() - 原地排序
numbers.sort()
print(numbers)  # [1, 1, 2, 3, 4, 5, 6, 9]

# sort(reverse=True) - 降序
numbers.sort(reverse=True)
print(numbers)  # [9, 6, 5, 4, 3, 2, 1, 1]

# sorted() - 返回新列表
nums = [3, 1, 4]
sorted_nums = sorted(nums)
print(sorted_nums)  # [1, 3, 4]
print(nums)         # [3, 1, 4]（原列表不变）

# reverse() - 反转
fruits = ["apple", "banana", "cherry"]
fruits.reverse()
print(fruits)  # ['cherry', 'banana', 'apple']
```

## 遍历列表

```python
fruits = ["apple", "banana", "cherry"]

# 遍历元素
for fruit in fruits:
    print(fruit)

# 遍历索引
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# enumerate()
for i, fruit in enumerate(fruits):
    print(f"{i}: {fruit}")

# 遍历多个列表
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
for name, age in zip(names, ages):
    print(f"{name} is {age}")
```

## 复制列表

```python
original = [1, 2, 3]

# 浅拷贝
copy1 = original.copy()
copy2 = original[:]
copy3 = list(original)

# 深拷贝（嵌套列表）
import copy
nested = [[1, 2], [3, 4]]
deep = copy.deepcopy(nested)
```

## 其他常用方法

```python
# len() - 长度
print(len([1, 2, 3]))  # 3

# max() / min() - 最大最小值
print(max([3, 1, 4]))  # 4
print(min([3, 1, 4]))  # 1

# sum() - 求和
print(sum([1, 2, 3]))  # 6

# any() / all()
print(any([False, True, False]))  # True
print(all([True, True, False]))   # False
```
