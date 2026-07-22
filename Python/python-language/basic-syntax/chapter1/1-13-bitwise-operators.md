# 位运算符

位运算符（Bitwise Operator）直接操作整数的二进制位，适用于底层编程、权限控制和性能优化。

## 位运算符列表

| 运算符 | 名称 | 说明 |
|--------|------|------|
| `&` | 按位与 | 两个位都为 1 时为 1 |
| `\|` | 按位或 | 两个位有一个为 1 时为 1 |
| `^` | 按位异或 | 两个位不同时为 1 |
| `~` | 按位取反 | 0 变 1，1 变 0 |
| `<<` | 左移 | 向左移动指定位数，低位补 0 |
| `>>` | 右移 | 向右移动指定位数，高位补符号位 |

## 按位与 &

```python
a = 0b1100  # 12
b = 0b1010  # 10

result = a & b  # 0b1000 = 8
print(f"{a:b} & {b:b} = {result:b} ({result})")
```

## 按位或 |

```python
a = 0b1100  # 12
b = 0b1010  # 10

result = a | b  # 0b1110 = 14
print(f"{a:b} | {b:b} = {result:b} ({result})")
```

## 按位异或 ^

```python
a = 0b1100  # 12
b = 0b1010  # 10

result = a ^ b  # 0b0110 = 6
print(f"{a:b} ^ {b:b} = {result:b} ({result})")
```

## 按位取反 ~

```python
a = 12  # 0b1100
result = ~a  # -13（补码表示）
print(f"~{a} = {result}")
```

## 左移 <<

```python
a = 3          # 0b0011
result = a << 2  # 0b1100 = 12
print(f"{a} << 2 = {result}")  # 相当于乘以 2²
```

## 右移 >>

```python
a = 16           # 0b10000
result = a >> 2   # 0b00100 = 4
print(f"{a} >> 2 = {result}")  # 相当于除以 2²
```

## 位运算应用

### 权限控制

```python
# 权限定义（使用 2 的幂）
READ = 1      # 0b001
WRITE = 2     # 0b010
EXECUTE = 4   # 0b100

# 分配权限（组合）
permissions = READ | WRITE  # 0b011 = 3

# 检查权限
has_read = permissions & READ    # True
has_write = permissions & WRITE  # True
has_exec = permissions & EXECUTE # False

print(f"权限: {permissions:03b}")
print(f"读: {bool(has_read)}, 写: {bool(has_write)}, 执行: {bool(has_exec)}")

# 添加权限
permissions |= EXECUTE
print(f"添加执行后: {permissions:03b}")

# 移除权限
permissions &= ~WRITE
print(f"移除写后: {permissions:03b}")
```

### 奇偶判断

```python
# 使用 & 1 判断奇偶（比 % 2 更快）
def is_odd(n):
    return n & 1 == 1

print(is_odd(5))   # True
print(is_odd(10))  # False
```

### 交换变量

```python
# 使用异或交换（无需临时变量）
a, b = 5, 9
a ^= b
b ^= a
a ^= b
print(f"交换后: a={a}, b={b}")  # a=9, b=5
```
