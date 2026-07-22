# bytes 与 bytearray 用法详解

## 基本方法

```python
b = b"Hello Python"

# 查找
print(b.find(b"Py"))     # 6
print(b.count(b"o"))     # 2

# 判断
print(b.startswith(b"He"))  # True
print(b.endswith(b"on"))    # True

# 转换
print(b.upper())  # b'HELLO PYTHON'
print(b.lower())  # b'hello python'

# 替换
print(b.replace(b"Python", b"World"))  # b'Hello World'

# 分割
print(b.split())  # [b'Hello', b'Python']
```

## bytearray 特有方法

```python
ba = bytearray(b"hello")

# 追加
ba.append(33)
print(ba)  # bytearray(b'hello!')

# 插入
ba.insert(0, 72)  # ASCII 'H'
print(ba)  # bytearray(b'Hello!')

# 删除
ba.pop()   # 删除最后一个
print(ba)  # bytearray(b'Hello')

# 移除
ba.remove(ord('l'))
print(ba)  # bytearray(b'Helo')

# 反转
ba.reverse()
print(ba)  # bytearray(b'oleH')

# 清空
ba.clear()
print(ba)  # bytearray(b'')
```

## 读写文件

```python
# 以二进制模式写入
with open("data.bin", "wb") as f:
    f.write(b"\x00\x01\x02\x03")
    f.write("你好".encode("utf-8"))

# 以二进制模式读取
with open("data.bin", "rb") as f:
    data = f.read()
    print(data.hex())  # 十六进制输出

# 清理
import os
os.remove("data.bin")
```
