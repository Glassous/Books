# VS Code 的 Python 配置

Visual Studio Code（简称 VS Code）是微软开发的免费、开源的代码编辑器，通过安装扩展可以成为强大的 Python 开发环境。

## 安装 VS Code

### 下载地址

访问 VS Code 官网下载：
- https://code.visualstudio.com/

支持 Windows、macOS、Linux 三大平台。

### 安装步骤

#### Windows
1. 运行下载的安装程序
2. 选择安装路径
3. 建议勾选：
   - 将"通过 Code 打开"操作添加到文件上下文菜单
   - 将"通过 Code 打开"操作添加到目录上下文菜单
   - 将 Code 注册为受支持的文件类型的编辑器
   - 添加到 PATH
4. 点击安装

#### macOS
1. 打开下载的 .zip 文件
2. 将 Visual Studio Code.app 拖动到 Applications 文件夹

#### Linux
```bash
# 使用 Snap 安装
sudo snap install code --classic

# 或使用 apt（Ubuntu/Debian）
sudo apt update
sudo apt install software-properties-common
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt install code
```

## 安装 Python 扩展

### 安装步骤

1. 打开 VS Code
2. 点击左侧活动栏的扩展图标（或按 `Ctrl+Shift+X`）
3. 搜索 "Python"
4. 选择 Microsoft 发布的 "Python" 扩展
5. 点击 "Install" 安装

### Python 扩展包含

Python 扩展会自动安装以下相关扩展：
- **Python**：核心 Python 支持
- **Pylance**：高性能语言服务器
- **Python Debugger**：调试支持
- **Jupyter**：Jupyter Notebook 支持

## 配置 Python 解释器

### 选择解释器

1. 按 `Ctrl+Shift+P` 打开命令面板
2. 输入 "Python: Select Interpreter"
3. 从列表中选择 Python 解释器
4. 如果未显示，点击 "Enter interpreter path..." 手动指定

### 手动指定解释器路径

#### Windows
```
C:\Python310\python.exe
C:\Users\用户名\AppData\Local\Programs\Python\Python310\python.exe
```

#### macOS
```
/usr/local/bin/python3
/opt/homebrew/bin/python3
```

#### Linux
```
/usr/bin/python3
/usr/local/bin/python3
```

## 工作区配置

### 创建项目文件夹

1. 点击 文件 -> 打开文件夹
2. 选择或创建项目文件夹
3. VS Code 会自动检测 Python 文件

### 工作区设置

在项目根目录创建 `.vscode/settings.json`：

```json
{
  "python.defaultInterpreterPath": "C:\\Python310\\python.exe",
  "python.linting.enabled": true,
  "python.linting.pylintEnabled": true,
  "python.formatting.provider": "black",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.organizeImports": true
  }
}
```

## 代码编辑功能

### 智能代码补全
- 输入时自动显示建议
- `Ctrl + Space` 手动触发补全
- 支持类型提示和文档字符串

### 代码导航
- `F12`：转到定义
- `Alt + F12`：查看定义
- `Ctrl + Shift + O`：转到符号
- `Ctrl + T`：转到工作区符号

### 代码重构
- `F2`：重命名符号
- `Ctrl+Shift+R`：重构菜单

## 调试配置

### 创建 launch.json

1. 点击左侧活动栏的调试图标
2. 点击 "create a launch.json file"
3. 选择 "Python File"

### 基本调试配置

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal",
      "justMyCode": true
    }
  ]
}
```

### 调试操作

- `F5`：启动调试
- `F9`：切换断点
- `F10`：单步跳过
- `F11`：单步进入
- `Shift+F11`：单步跳出

## 代码格式化

### 安装格式化工具

```bash
# 安装 Black
pip install black

# 安装 autopep8
pip install autopep8

# 安装 yapf
pip install yapf
```

### 配置格式化工具

在 `settings.json` 中配置：

```json
{
  "python.formatting.provider": "black",
  "python.formatting.blackArgs": [
    "--line-length",
    "88"
  ],
  "editor.formatOnSave": true
}
```

## 代码检查

### 安装 Linter

```bash
# 安装 Pylint
pip install pylint

# 安装 Flake8
pip install flake8

# 安装 Mypy（类型检查）
pip install mypy
```

### 配置 Linter

```json
{
  "python.linting.enabled": true,
  "python.linting.pylintEnabled": true,
  "python.linting.flake8Enabled": true,
  "python.linting.mypyEnabled": true
}
```

## 常用快捷键

| 功能 | Windows/Linux | macOS |
|------|---------------|-------|
| 命令面板 | Ctrl+Shift+P | Cmd+Shift+P |
| 快速打开 | Ctrl+P | Cmd+P |
| 打开设置 | Ctrl+, | Cmd+, |
| 集成终端 | Ctrl+` | Cmd+` |
| 运行代码 | Ctrl+F5 | Cmd+F5 |
| 切换终端 | Ctrl+` | Cmd+` |
| 注释 | Ctrl+/ | Cmd+/ |
| 格式化 | Shift+Alt+F | Shift+Option+F |

## 推荐扩展

### Python 相关
- **Python**：官方 Python 扩展
- **Pylance**：高性能语言服务器
- **Python Debugger**：调试支持
- **Jupyter**：Notebook 支持

### 代码质量
- **Prettier**：代码格式化
- **ESLint**：JavaScript/TypeScript 检查
- **GitLens**：Git 增强

### 主题和外观
- **One Dark Pro**：暗色主题
- **Material Icon Theme**：文件图标主题
- **Bracket Pair Colorizer**：括号颜色匹配

### 其他实用
- **Live Server**：本地开发服务器
- **REST Client**：API 测试
- **Docker**：Docker 支持

## 常见问题

### Python 扩展未检测到解释器
- 确认 Python 已安装并添加到 PATH
- 手动指定解释器路径
- 重启 VS Code

### 代码补全不工作
- 检查 Pylance 扩展是否安装
- 确认 Python 解释器已正确选择
- 检查工作区设置

### 调试器无法启动
- 检查 launch.json 配置
- 确认脚本路径正确
- 检查 Python 解释器配置

### 格式化不生效
- 确认格式化工具已安装
- 检查 settings.json 配置
- 确认已启用保存时格式化
