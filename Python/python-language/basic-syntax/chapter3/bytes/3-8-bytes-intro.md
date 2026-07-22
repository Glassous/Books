# bytes 与 bytearray 介绍

`bytes` 和 `bytearray` 是用于处理二进制数据的序列类型。

## bytes

不可变的字节序列：

```python
# 字面量
b1 = b"hello"
print(b1)        # b'hello'
print(type(b1))  # <class 'bytes'>

# 从列表创建
b2 = bytes([65, 66, 67])
print(b2)  # b'ABC'

# 指定长度（填充 0）
b3 = bytes(5)
print(b3)  # b'\x00\x00\x00\x00\x00'

# 十六进制
b4 = bytes.fromhex("48656c6c6f")
print(b4)  # b'Hello'
```

## bytearray

可变的字节序列：

```python
# 从字符串创建
ba = bytearray(b"hello")
print(ba)  # bytearray(b'hello')

# 修改
ba[0] = 72  # ASCII 'H'
print(ba)  # bytearray(b'Hello')

# 追加
ba.append(33)  # ASCII '!'
print(ba)  # bytearray(b'Hello!')

# 从列表创建
ba2 = bytearray([65, 66, 67])
print(ba2)  # bytearray(b'ABC')
```

## 特性

```python
# 支持索引和切片
b = b"Python"
print(b[0])      # 80（整数，不是字符）
print(b[0:3])    # b'Pyt'

# 支持 in 操作
print(80 in b)   # True（80 是 'P' 的 ASCII）
print(b"Py" in b)  # True

# 不可变 vs 可变
# b[0] = 74      # TypeError: 'bytes' object does not support item assignment
ba = bytearray(b)
ba[0] = 74       # 可以修改
print(ba)        # bytearray(b'Jython')
```

## 编码与解码

```python
# str -> bytes（编码）
text = "你好"
encoded = text.encode("utf-8")
print(encoded)  # b'\xe4\xbd\xa0\xe5\xa5\xbd'

# bytes -> str（解码）
decoded = encoded.decode("utf-8")
print(decoded)  # 你好
```
