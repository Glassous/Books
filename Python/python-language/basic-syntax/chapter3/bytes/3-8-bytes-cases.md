# bytes 与 bytearray 案例

## 案例一：简单加密

```python
def xor_encrypt(data: bytes, key: bytes) -> bytes:
    """使用 XOR 加密/解密"""
    result = bytearray(data)
    for i in range(len(result)):
        result[i] ^= key[i % len(key)]
    return bytes(result)

message = b"Hello, Python!"
key = b"key"

encrypted = xor_encrypt(message, key)
decrypted = xor_encrypt(encrypted, key)

print(f"原文: {message}")
print(f"加密: {encrypted.hex()}")
print(f"解密: {decrypted}")
```

## 案例二：图片头部检测

```python
def detect_image_type(data: bytes) -> str:
    """检测图片类型（根据文件签名）"""
    if data[:2] == b"\xff\xd8":
        return "JPEG"
    elif data[:4] == b"\x89PNG":
        return "PNG"
    elif data[:2] == b"BM":
        return "BMP"
    elif data[:4] == b"GIF8":
        return "GIF"
    return "未知"

# 模拟数据
jpeg_header = b"\xff\xd8\xff\xe0" + b"\x00" * 10
png_header = b"\x89PNG\r\n\x1a\n" + b"\x00" * 10

print(detect_image_type(jpeg_header))  # JPEG
print(detect_image_type(png_header))   # PNG
```

## 案例三：网络数据封包

```python
import struct

def pack_message(type_id: int, content: str) -> bytes:
    """打包消息：1字节类型 + 4字节长度 + 内容"""
    content_bytes = content.encode("utf-8")
    header = struct.pack("!BI", type_id, len(content_bytes))
    return header + content_bytes

def unpack_message(data: bytes):
    """解包消息"""
    type_id = data[0]
    content_len = struct.unpack("!I", data[1:5])[0]
    content = data[5:5+content_len].decode("utf-8")
    return type_id, content

packet = pack_message(1, "Hello")
print(f"封包: {packet.hex()}")
type_id, content = unpack_message(packet)
print(f"类型: {type_id}, 内容: {content}")
```
