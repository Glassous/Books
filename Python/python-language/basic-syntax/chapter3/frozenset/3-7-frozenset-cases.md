# frozenset 案例

## 案例一：标签系统

```python
# 使用 frozenset 表示文章标签（不可变，适合缓存）
articles = {
    frozenset(["python", "tutorial"]): "Python 基础教程",
    frozenset(["python", "oop"]): "Python 面向对象",
    frozenset(["data", "science"]): "数据科学入门",
}

def find_articles(tags):
    key = frozenset(tags)
    return articles.get(key, "未找到")

print(find_articles(["python", "tutorial"]))  # Python 基础教程
print(find_articles(["python", "oop"]))        # Python 面向对象
```

## 案例二：权限组

```python
# 使用 frozenset 表示固定的权限组
READ_ONLY = frozenset(["read"])
STANDARD = frozenset(["read", "write"])
ADMIN = frozenset(["read", "write", "delete", "admin"])

def check_permission(user_group, required):
    """检查用户组是否有指定权限"""
    return required in user_group

print(check_permission(STANDARD, "write"))     # True
print(check_permission(READ_ONLY, "delete"))   # False
```

## 案例三：去重且可哈希

```python
# 对列表去重后转为 frozenset
def unique_frozenset(items):
    return frozenset(items)

# 用于去重统计
data = [
    [1, 2, 3],
    [3, 2, 1],
    [4, 5, 6],
    [1, 2, 3]
]
unique = {frozenset(item) for item in data}
print(unique)  # {frozenset({1, 2, 3}), frozenset({4, 5, 6})}
```
