# range 案例

## 案例一：乘法表

```python
for i in range(1, 10):
    for j in range(1, i + 1):
        print(f"{j}x{i}={i*j}", end="\t")
    print()
```

## 案例二：数字统计

```python
# 统计 1-100 中的奇数和偶数
odds = list(range(1, 101, 2))
evens = list(range(2, 101, 2))
print(f"奇数个数: {len(odds)}")
print(f"偶数个数: {len(evens)}")
print(f"奇数和: {sum(odds)}")
print(f"偶数和: {sum(evens)}")
```

## 案例三：分页

```python
def paginate(items, page, page_size=10):
    start = (page - 1) * page_size
    end = start + page_size
    return items[start:end]

items = list(range(1, 51))
print(f"第1页: {paginate(items, 1)}")
print(f"第3页: {paginate(items, 3)}")
```
