# 汉诺塔

汉诺塔（Tower of Hanoi）是经典的递归问题，目标是将所有盘子从 A 柱移动到 C 柱，每次只能移动一个盘子，且大盘不能放在小盘上。

## 递归思路

- 将 n-1 个盘子从 A 经 C 移到 B
- 将第 n 个盘子从 A 移到 C
- 将 n-1 个盘子从 B 经 A 移到 C

## 递归实现

```python
def hanoi(n, source, target, auxiliary):
    """
    汉诺塔递归解法

    参数:
        n: 盘子数量
        source: 起始柱
        target: 目标柱
        auxiliary: 辅助柱
    """
    if n == 1:
        print(f"移动盘子 1: {source} -> {target}")
        return

    # 将 n-1 个盘子从 source 移到 auxiliary
    hanoi(n - 1, source, auxiliary, target)

    # 移动第 n 个盘子
    print(f"移动盘子 {n}: {source} -> {target}")

    # 将 n-1 个盘子从 auxiliary 移到 target
    hanoi(n - 1, auxiliary, target, source)

# 3 个盘子的解法
print("3 个盘子的解法:")
hanoi(3, "A", "C", "B")
```

## 计算移动次数

```python
def hanoi_count(n):
    """计算汉诺塔所需移动次数"""
    if n == 1:
        return 1
    return 2 * hanoi_count(n - 1) + 1

# 更简单的公式：2^n - 1
def hanoi_formula(n):
    return 2 ** n - 1

for i in range(1, 10):
    print(f"{i} 个盘子需要 {hanoi_count(i)} 步（公式验证: {hanoi_formula(i)}）")
```

## 带步骤编号的实现

```python
def hanoi_steps(n, source, target, auxiliary):
    """带步骤编号的汉诺塔"""
    steps = []

    def move(n, source, target, auxiliary):
        if n == 1:
            steps.append(f"移动盘子 1: {source} -> {target}")
            return
        move(n - 1, source, auxiliary, target)
        steps.append(f"移动盘子 {n}: {source} -> {target}")
        move(n - 1, auxiliary, target, source)

    move(n, source, target, auxiliary)
    return steps

print("\n4 个盘子的完整步骤:")
steps = hanoi_steps(4, "A", "C", "B")
for i, step in enumerate(steps, 1):
    print(f"第{i:2d}步: {step}")
```

## 可视化状态

```python
def hanoi_visual(n):
    """可视化汉诺塔移动过程"""
    # 初始化三个柱子
    pegs = {
        'A': list(range(n, 0, -1)),
        'B': [],
        'C': []
    }

    def print_state():
        print(f"A: {pegs['A']}")
        print(f"B: {pegs['B']}")
        print(f"C: {pegs['C']}")
        print("-" * 20)

    def move_disk(source, target):
        disk = pegs[source].pop()
        pegs[target].append(disk)
        print(f"移动盘子 {disk}: {source} -> {target}")
        print_state()

    def solve(n, source, target, auxiliary):
        if n == 1:
            move_disk(source, target)
            return

        solve(n - 1, source, auxiliary, target)
        move_disk(source, target)
        solve(n - 1, auxiliary, target, source)

    print("初始状态:")
    print_state()
    solve(n, 'A', 'C', 'B')
    print("完成！")

print("3 个盘子的可视化:")
hanoi_visual(3)
```
