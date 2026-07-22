# frozenset 介绍

`frozenset` 是不可变的集合，创建后不能添加或删除元素。可作为字典的键或放入其他集合中。

## 创建 frozenset

```python
# 从列表创建
fs1 = frozenset([1, 2, 3, 3, 4])
print(fs1)  # frozenset({1, 2, 3, 4})

# 从字符串创建
fs2 = frozenset("hello")
print(fs2)  # frozenset({'h', 'e', 'l', 'o'})

# 空 frozenset
empty = frozenset()
print(empty)  # frozenset()

# 从 set 创建
s = {1, 2, 3}
fs3 = frozenset(s)
```

## 特性

```python
# 不可变
fs = frozenset([1, 2, 3])
# fs.add(4)  # AttributeError

# 可以作为字典的键
d = {frozenset([1, 2]): "A", frozenset([3, 4]): "B"}
print(d)  # {frozenset({1, 2}): 'A', frozenset({3, 4}): 'B'}

# 可以作为集合的元素
s = set()
s.add(frozenset([1, 2]))
s.add(frozenset([3, 4]))
print(s)  # {frozenset({3, 4}), frozenset({1, 2})}
```

## 与 set 对比

```python
# 可变性
s = {1, 2, 3}
s.add(4)           # 可以修改

fs = frozenset([1, 2, 3])
# fs.add(4)        # 不可修改

# hashable
# hash(s)          # TypeError: unhashable type: 'set'
print(hash(fs))    # 有哈希值

# 使用场景
# set: 需要频繁增删的场景
# frozenset: 需要作为键或常量的场景
```
