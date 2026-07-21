# 环境配置

本节将介绍如何在不同操作系统上安装和配置 Python 开发环境。

## 下载 Python

### 官方下载地址

访问 Python 官方网站下载最新版本：
- 官网：https://www.python.org/downloads/
- 推荐下载 Python 3.10+ 版本

### 选择版本

建议选择最新的稳定版本。下载时注意选择正确的系统架构（32位或64位）。

## Windows 系统安装

### 安装步骤

1. 运行下载的安装程序（.exe 文件）
2. **重要**：勾选 "Add Python to PATH" 选项
3. 选择 "Customize installation" 可自定义安装路径
4. 点击 "Install" 开始安装

### 验证安装

打开命令提示符（cmd）或 PowerShell，输入：

```bash
python --version
```

如果显示 Python 版本号，说明安装成功。

同时检查 pip 是否安装：

```bash
pip --version
```

### 环境变量配置（如未自动添加）

1. 右键点击 "此电脑" -> "属性" -> "高级系统设置"
2. 点击 "环境变量"
3. 在 "系统变量" 中找到 "Path"，点击 "编辑"
4. 添加 Python 安装路径和 Scripts 路径：
   ```
   C:\Python310\
   C:\Python310\Scripts\
   ```

## macOS 系统安装

### 使用 Homebrew 安装（推荐）

```bash
# 安装 Homebrew（如未安装）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 安装 Python
brew install python
```

### 使用官方安装包

1. 从官网下载 macOS 安装包
2. 双击运行安装程序
3. 按照提示完成安装

### 验证安装

```bash
python3 --version
pip3 --version
```

## Linux 系统安装

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install python3 python3-pip
```

### CentOS/RHEL

```bash
sudo yum install python3
```

### 验证安装

```bash
python3 --version
pip3 --version
```

## 虚拟环境配置

### 为什么需要虚拟环境

虚拟环境可以为每个项目创建独立的 Python 环境，避免不同项目之间的依赖冲突。

### 创建虚拟环境

```bash
# 使用 venv 模块（Python 3 内置）
python -m venv myenv

# 激活虚拟环境
# Windows
myenv\Scripts\activate

# macOS/Linux
source myenv/bin/activate
```

### 退出虚拟环境

```bash
deactivate
```

## 包管理工具 pip

### 常用命令

```bash
# 安装包
pip install package_name

# 安装指定版本
pip install package_name==1.0.0

# 升级包
pip install --upgrade package_name

# 卸载包
pip uninstall package_name

# 查看已安装的包
pip list

# 导出依赖
pip freeze > requirements.txt

# 从文件安装依赖
pip install -r requirements.txt
```

### 使用国内镜像源

国内用户可以配置镜像源以加速下载：

```bash
# 临时使用
pip install package_name -i https://pypi.tuna.tsinghua.edu.cn/simple

# 永久配置
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

## 验证环境配置

创建一个测试文件 `test.py`：

```python
import sys
print(f"Python 版本: {sys.version}")
print(f"Python 路径: {sys.executable}")

import pip
print(f"pip 版本: {pip.__version__}")
```

运行测试：

```bash
python test.py
```

如果能正确显示版本信息，说明 Python 环境配置成功。
