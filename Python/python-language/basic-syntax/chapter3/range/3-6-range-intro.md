# range 介绍

`range` 表示一个不可变的整数序列，常用于 `for` 循环中生成数字。

## 创建 range

```python
# range(stop)：0 到 stop-1
r1 = range(5)
print(list(r1))  # [0, 1, 2, 3, 4]

# range(start, stop)：start 到 stop-1
r2 = range(2, 7)
print(list(r2))  # [2, 3, 4, 5, 6]

# range(start, stop, step)：带步长
r3 = range(0, 10, 2)
print(list(r3))  # [0, 2, 4, 6, 8]

# 负步长（递减）
r4 = range(10, 0, -2)
print(list(r4))  # [10, 8, 6, 4, 2]
```

## 特性

```python
# 不可变
r = range(5)
# r[0] = 10  # TypeError

# 支持索引和切片
print(r[0])     # 0
print(r[-1])    # 4
print(list(r[1:4]))  # [1, 2, 3]

# 支持 in 操作
print(3 in r)   # True
print(10 in r)  # False

# 支持 len()
print(len(r))   # 5
```

## 内存优势

`range` 不存储所有值，而是惰性计算：

```python
# range 占用固定内存
r = range(1_000_000)
print(sys.getsizeof(r))  # 48 字节（无论多大）

# 等价的列表占用大量内存
lst = list(range(1_000_000))
print(sys.getsizeof(lst))  # 约 8MB
```
