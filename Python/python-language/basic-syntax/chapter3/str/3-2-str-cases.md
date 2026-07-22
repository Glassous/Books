# 字符串案例

## 案例一：文本统计分析

```python
def analyze_text(text):
    lines = text.splitlines()
    words = text.split()
    chars = len(text)

    # 统计各类字符
    letter_count = sum(1 for c in text if c.isalpha())
    digit_count = sum(1 for c in text if c.isdigit())
    space_count = sum(1 for c in text if c.isspace())
    punct_count = chars - letter_count - digit_count - space_count

    # 单词统计
    word_lengths = [len(w.strip(".,!?;:\"'")) for w in words]
    avg_word_length = sum(word_lengths) / len(word_lengths) if words else 0

    # 找出最长单词
    longest = max(words, key=lambda w: len(w.strip(".,!?;:\"'"))).strip(".,!?;:\"'")\
        if words else ""

    return {
        "行数": len(lines),
        "单词数": len(words),
        "字符数": chars,
        "字母数": letter_count,
        "数字数": digit_count,
        "空格数": space_count,
        "标点数": punct_count,
        "平均词长": round(avg_word_length, 2),
        "最长单词": longest
    }

text = """Hello World! Python is great.
I have 2 cats and 3 dogs.
Learning Python in 2024."""

stats = analyze_text(text)
for key, value in stats.items():
    print(f"{key}: {value}")
```

## 案例二：密码强度检测

```python
def check_password_strength(password):
    score = 0
    feedback = []

    if len(password) >= 8:
        score += 1
    else:
        feedback.append("长度至少8位")

    if any(c.isupper() for c in password):
        score += 1
    else:
        feedback.append("需要大写字母")

    if any(c.islower() for c in password):
        score += 1
    else:
        feedback.append("需要小写字母")

    if any(c.isdigit() for c in password):
        score += 1
    else:
        feedback.append("需要数字")

    special = "!@#$%^&*"
    if any(c in special for c in password):
        score += 1
    else:
        feedback.append("需要特殊字符")

    levels = {5: "非常强", 4: "强", 3: "中等", 2: "弱", 1: "很弱", 0: "极弱"}
    return levels.get(score, "极弱"), feedback

test_passwords = ["abc", "Hello123", "Str0ng!Pass", "weak"]
for pwd in test_passwords:
    level, tips = check_password_strength(pwd)
    print(f"'{pwd}': {level}")
    if tips:
        print(f"  改进建议: {', '.join(tips)}")
```

## 案例三：URL 解析

```python
def parse_url(url):
    result = {}

    # 提取协议
    if "://" in url:
        result["protocol"], url = url.split("://", 1)
    else:
        result["protocol"] = ""

    # 提取域名和路径
    if "/" in url:
        result["domain"], result["path"] = url.split("/", 1)
        result["path"] = "/" + result["path"]
    else:
        result["domain"] = url
        result["path"] = ""

    # 提取端口
    if ":" in result["domain"]:
        domain, port = result["domain"].split(":", 1)
        result["domain"] = domain
        result["port"] = int(port)
    else:
        result["port"] = 443 if result["protocol"] == "https" else 80

    # 提取查询参数
    if "?" in result["path"]:
        path, query_string = result["path"].split("?", 1)
        result["path"] = path
        params = {}
        for param in query_string.split("&"):
            if "=" in param:
                key, value = param.split("=", 1)
                params[key] = value
        result["params"] = params
    else:
        result["params"] = {}

    return result

url = "https://api.example.com:8080/users?id=123&name=Alice"
parsed = parse_url(url)
for key, value in parsed.items():
    print(f"{key}: {value}")
```

## 案例四：日志分析

```python
import re

logs = """2024-01-15 10:30:45 [INFO] 用户登录成功: alice
2024-01-15 10:31:20 [ERROR] 数据库连接失败: timeout
2024-01-15 10:32:10 [INFO] 用户登出: alice
2024-01-15 10:33:00 [WARN] 磁盘空间不足: 85%
2024-01-15 10:34:15 [ERROR] 服务无响应: port 8080"""

def parse_logs(log_text):
    entries = []
    for line in log_text.splitlines():
        parts = line.split(" ", 3)
        if len(parts) >= 4:
            date = parts[0]
            time = parts[1]
            level = parts[2].strip("[]")
            message = parts[3]
            entries.append({"date": date, "time": time,
                          "level": level, "message": message})
    return entries

def analyze_logs(entries):
    stats = {"INFO": 0, "WARN": 0, "ERROR": 0, "DEBUG": 0}
    errors = []
    for entry in entries:
        stats[entry["level"]] = stats.get(entry["level"], 0) + 1
        if entry["level"] == "ERROR":
            errors.append(entry["message"])
    return stats, errors

entries = parse_logs(logs)
stats, errors = analyze_logs(entries)

print("日志统计:")
for level, count in stats.items():
    print(f"  {level}: {count}")

if errors:
    print("\n错误列表:")
    for err in errors:
        print(f"  - {err}")
```

## 案例五：模板引擎

```python
def simple_template(template, **kwargs):
    result = template
    for key, value in kwargs.items():
        placeholder = "{{" + key + "}}"
        result = result.replace(placeholder, str(value))
    return result

def render_list(template, items):
    start = template.find("{% for item in items %}")
    end = template.find("{% endfor %}")
    if start == -1 or end == -1:
        return template

    item_template = template[start + len("{% for item in items %}"):end]
    rendered_items = []

    for item in items:
        rendered = item_template.replace("{{item}}", str(item))
        rendered_items.append(rendered)

    result = template[:start] + "".join(rendered_items) + template[end + len("{% endfor %}"):]
    return result

# 简单模板
template = "Hello, {{name}}! You are {{age}} years old."
print(simple_template(template, name="Alice", age=25))

# 列表模板
list_template = "Items:\n{% for item in items %}- {{item}}\n{% endfor %}"
print(render_list(list_template, ["Apple", "Banana", "Cherry"]))
```

## 案例六：文件路径处理

```python
def path_info(path):
    # 处理路径分隔符
    path = path.replace("\\", "/")

    parts = path.rsplit("/", 1)
    if len(parts) == 2:
        directory, filename = parts
    else:
        directory, filename = "", parts[0]

    if "." in filename:
        name, ext = filename.rsplit(".", 1)
    else:
        name, ext = filename, ""

    return {
        "full_path": path,
        "directory": directory or "/",
        "filename": filename,
        "name": name,
        "extension": "." + ext if ext else "",
        "is_hidden": filename.startswith(".")
    }

paths = [
    "/home/user/docs/report.pdf",
    "C:/Users/Admin/.config/settings.json",
    "/var/log/system.log",
]

for p in paths:
    info = path_info(p)
    print(f"\n{p}")
    for key, value in info.items():
        print(f"  {key}: {value}")
```
