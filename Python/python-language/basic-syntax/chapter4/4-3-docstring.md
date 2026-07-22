# 函数说明文档

文档字符串（Docstring）用于描述函数的功能、参数和返回值，位于函数定义的第一行。

## 单行文档字符串

```python
def add(a, b):
    """返回两个数的和"""
    return a + b
```

## 多行文档字符串

```python
def calculate_bmi(weight, height):
    """
    计算 BMI（身体质量指数）

    参数:
        weight: 体重（公斤）
        height: 身高（米）

    返回:
        float: BMI 值
    """
    return weight / (height ** 2)
```

## 访问文档字符串

```python
def add(a, b):
    """返回两个数的和"""
    return a + b

# 使用 __doc__
print(add.__doc__)  # 返回两个数的和

# 使用 help()
help(add)
```

## Google 风格文档字符串

```python
def connect_to_database(host, port=3306, timeout=30):
    """
    连接到数据库服务器

    Args:
        host (str): 数据库主机地址
        port (int, optional): 端口号，默认 3306
        timeout (int): 连接超时时间（秒）

    Returns:
        bool: 连接成功返回 True，失败返回 False

    Raises:
        ConnectionError: 当连接失败时抛出

    Example:
        >>> connect_to_database("localhost")
        True
    """
    return True
```

## NumPy 风格文档字符串

```python
def analyze_data(data):
    """
    分析数据集的基本统计信息

    Parameters
    ----------
    data : list
        待分析的数据列表

    Returns
    -------
    dict
        包含 mean（均值）、std（标准差）、min、max 的字典

    Examples
    --------
    >>> analyze_data([1, 2, 3, 4, 5])
    {'mean': 3.0, 'std': 1.41, 'min': 1, 'max': 5}
    """
    mean = sum(data) / len(data)
    variance = sum((x - mean) ** 2 for x in data) / len(data)
    return {
        "mean": mean,
        "std": variance ** 0.5,
        "min": min(data),
        "max": max(data)
    }
```

## 编写规范

```python
def search_users(keyword, page=1, limit=20):
    """
    搜索用户

    根据关键字搜索用户，支持分页查询。

    Args:
        keyword (str): 搜索关键字
        page (int): 页码，从 1 开始
        limit (int): 每页返回数量，最大 100

    Returns:
        list[dict]: 用户信息列表

    注意:
        未登录用户只能搜索公开信息
    """
    return []
```

文档字符串不仅仅是注释，还可以通过工具生成 API 文档，是代码可读性的重要组成部分。
