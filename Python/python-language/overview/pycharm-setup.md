# PyCharm 安装与配置

PyCharm 是 JetBrains 公司开发的专业 Python IDE，提供智能代码补全、代码分析、调试、测试等强大功能。

## PyCharm 版本选择

### 社区版（Community）
- 免费开源
- 支持 Python 开发的核心功能
- 适合学习和个人项目

### 专业版（Professional）
- 付费软件（提供 30 天试用）
- 支持 Web 开发、数据库工具、远程开发等高级功能
- 适合专业开发和企业项目

## 下载 PyCharm

### 官方下载地址

访问 JetBrains 官网：
- https://www.jetbrains.com/pycharm/download/

根据操作系统选择对应版本下载。

## Windows 系统安装

### 安装步骤

1. 运行下载的安装程序（.exe 文件）
2. 点击 "Next" 选择安装路径
3. 在安装选项界面，建议勾选：
   - 创建桌面快捷方式（64位）
   - 将 "bin" 目录添加到 PATH
   - 关联 .py 文件
4. 点击 "Install" 开始安装
5. 完成安装后，选择立即重启或稍后重启

### 首次启动配置

1. 启动 PyCharm，选择不导入设置
2. 选择 UI 主题（Darcula 暗色主题推荐）
3. 创建或打开项目

## macOS 系统安装

### 安装步骤

1. 打开下载的 .dmg 文件
2. 将 PyCharm 图标拖动到 Applications 文件夹
3. 从启动台或应用程序文件夹启动 PyCharm

## Linux 系统安装

### 使用 Snap 安装（推荐）

```bash
sudo snap install pycharm-community --classic
```

### 使用 tar.gz 安装

```bash
# 解压
tar -xzf pycharm-community-*.tar.gz

# 进入目录运行
cd pycharm-community-*/bin
./pycharm.sh
```

## 配置 Python 解释器

### 配置步骤

1. 打开 PyCharm，进入项目
2. 点击菜单：File -> Settings（macOS: PyCharm -> Preferences）
3. 导航到：Project -> Python Interpreter
4. 点击齿轮图标，选择 "Add"
5. 选择解释器类型：
   - **System Interpreter**：使用系统安装的 Python
   - **Virtualenv Environment**：使用虚拟环境
   - **Conda Environment**：使用 Anaconda 环境

### 选择 Python 解释器

- 如果已安装 Python，PyCharm 通常会自动检测
- 可以手动指定 Python 可执行文件路径
- Windows：`C:\Python310\python.exe`
- macOS/Linux：`/usr/bin/python3` 或 `/usr/local/bin/python3`

## 创建第一个项目

### 新建项目

1. 点击 "New Project"
2. 选择项目位置和解释器
3. 点击 "Create" 创建项目

### 创建 Python 文件

1. 右键点击项目目录
2. 选择 New -> Python File
3. 输入文件名（如 `hello.py`）

### 编写并运行代码

```python
print("Hello, PyCharm!")
```

右键点击编辑器，选择 "Run 'hello'" 运行代码。

## 常用功能

### 代码补全
- 输入时自动显示建议列表
- 按 `Tab` 或 `Enter` 接受建议
- `Ctrl + Space` 手动触发补全

### 代码导航
- `Ctrl + Click`：跳转到定义
- `Alt + Left/Right`：在历史位置间导航
- `Ctrl + Shift + F`：全局搜索

### 调试功能
- 点击行号左侧设置断点
- 点击调试按钮启动调试
- 使用调试工具栏控制执行流程

### 代码格式化
- `Ctrl + Alt + L`：格式化代码
- 自动遵循 PEP 8 规范

## 常用快捷键

| 功能 | Windows/Linux | macOS |
|------|---------------|-------|
| 运行 | Shift + F10 | Ctrl + R |
| 调试 | Shift + F9 | Ctrl + D |
| 查找 | Ctrl + F | Cmd + F |
| 替换 | Ctrl + R | Cmd + R |
| 注释 | Ctrl + / | Cmd + / |
| 复制行 | Ctrl + D | Cmd + D |
| 删除行 | Ctrl + Y | Cmd + Backspace |

## 插件推荐

### 中文语言包
- 安装路径：Settings -> Plugins -> 搜索 "Chinese"
- 适合中文用户使用

### 其他推荐插件
- **Translation**：翻译插件
- **Rainbow Brackets**：彩虹括号
- **Key Promoter X**：快捷键提示

## 常见问题

### 解释器未检测到
- 确认 Python 已正确安装
- 手动添加解释器路径

### 导入模块报错
- 检查是否选择了正确的解释器
- 确认模块已安装在对应环境中

### 运行配置问题
- 检查 Run Configuration 设置
- 确认脚本路径正确
