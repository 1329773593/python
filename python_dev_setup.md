为了帮助大家顺利搭建 Python 开发环境，以下是详细的开发环境搭建指南，涵盖 Python、VSCode 和 Git 的安装与配置。该指南适用于初学者，旨在提供清晰、实用的步骤，帮助大家快速上手开发。([apifox][1])

---

# 🛠️ Python 开发环境搭建指南

## 🐍 第一部分：安装 Python

### 1. 下载 Python 安装包

* **官方网站**：访问 [Python 官网](https://www.python.org/downloads/) 下载适用于你操作系统的最新版本。

### 2. 安装 Python

* **安装步骤**：

  1. 双击下载的安装包，启动安装程序。
  2. **勾选**“Add Python to PATH”选项。
  3. 点击“Customize installation”进行自定义安装。
  4. 在“Advanced Options”中，**勾选**“Install for all users”并选择安装路径。
  5. 点击“Install”开始安装。([cnblogs.com][2], [CSDN 博客][3])

* **注意事项**：

  * 确保选择正确的操作系统版本（32 位或 64 位）。
  * 安装过程中，**勾选**“Install launcher for all users”和“Add Python to PATH”选项。
  * 建议使用 Python 3.x 版本，Python 2.x 已停止支持。([cnblogs.com][4], [cnblogs.com][2])

### 3. 切换镜像源（可选）

由于国内访问 Python 官方源可能较慢，建议切换至国内镜像源。

* **阿里云镜像**：

```bash
  pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
```



* **清华大学镜像**：

```bash
  pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/
```



### 4. 安装常用 Python 包

常用的 Python 包包括：

* `numpy`：用于科学计算。
* `pandas`：用于数据处理和分析。
* `matplotlib`：用于绘图。
* `scikit-learn`：用于机器学习。
* `tensorflow` 或 `torch`：用于深度学习。

安装命令示例：

```bash
pip install numpy pandas matplotlib scikit-learn
```



### 5. 创建虚拟环境

为了避免包版本冲突，建议为每个项目创建独立的虚拟环境。

* **创建虚拟环境**：

```bash
  python -m venv venv
```



* **激活虚拟环境**：

  * Windows：

    ```bash
    .\venv\Scripts\activate
    ```
  * macOS/Linux：([cnblogs.com][4])

    ```bash
    source venv/bin/activate
    ```

* **退出虚拟环境**：

```bash
  deactivate
```



---

## 💻 第二部分：安装 VSCode

### 1. 下载 VSCode

* **官方网站**：访问 [VSCode 官网](https://code.visualstudio.com/) 下载适用于你操作系统的最新版本。([apifox][1])

### 2. 安装 VSCode

* **安装步骤**：

  1. 双击下载的安装包，启动安装程序。
  2. 按照提示完成安装。([cnblogs.com][2])

### 3. 安装插件

在 VSCode 中，插件可以增强编辑器的功能。

* **常用插件**：

  * **Python**：提供 Python 语法高亮、自动补全、调试等功能。
  * **Pylance**：提供更快的 IntelliSense 和类型检查。
  * **Jupyter**：支持 Jupyter Notebook 的编辑和运行。
  * **Markdown All in One**：增强 Markdown 编辑体验。
  * **GitLens**：增强 Git 功能。([apifox][1])

安装方法：

1. 打开 VSCode。
2. 点击左侧活动栏的扩展图标（或按 `Ctrl+Shift+X`）。
3. 在搜索框中输入插件名称，点击“安装”按钮。([apifox][1])

---

## 🧾 第三部分：安装 Git

### 1. 下载 Git

* **官方网站**：访问 [Git 官网](https://git-scm.com/) 下载适用于你操作系统的最新版本。

### 2. 安装 Git

* **安装步骤**：

  1. 双击下载的安装包，启动安装程序。
  2. 按照提示完成安装。

### 3. 配置 Git

* **设置用户名和邮箱**：

```bash
  git config --global user.name "Your Name"
  git config --global user.email "youremail@example.com"
```



* **查看配置**：

```bash
  git config --list
```



### 4. 克隆仓库

使用 `git clone` 命令将远程仓库复制到本地：

```bash
git clone https://gitee.com/Python_Ai_Road/eat_pytorch_in_20_days
```



### 5. 常用 Git 命令

* **查看当前状态**：

```bash
  git status
```



* **查看当前分支**：

```bash
  git branch
```



* **切换分支**：

```bash
  git checkout <branch_name>
```



* **添加文件到暂存区**：

```bash
  git add <file_name>
```



* **提交更改**：

```bash
  git commit -m "Commit message"
```



* **推送更改到远程仓库**：

```bash
  git push origin <branch_name>
```



* **拉取远程仓库的更改**：

```bash
  git pull origin <branch_name>
```



---

## 📦 常用 Python 库

以下是一些常用的 Python 库，适用于数据分析、机器学习、深度学习等领域：

* **数据处理**：

  * `numpy`：用于科学计算。
  * `pandas`：用于数据处理和分析。

* **数据可视化**：

  * `matplotlib`：用于绘图。
  * `seaborn`：基于 `matplotlib` 的统计数据可视化库。

* **机器学习**：

  * `scikit-learn`：用于机器学习。
  * `xgboost`：用于梯度提升树模型。

* **深度学习**：

  * `tensorflow`：用于深度学习。
  * `torch`：PyTorch，深度学习框架。

* **Web 开发**：

  * `flask`：轻量级 Web 框架。
  * `django`：全功能 Web 框架。

安装方法：

```bash
pip install numpy pandas matplotlib scikit-learn
```



---

## 📄 常用 VSCode 插件

以下是一些常用的 VSCode 插件，适用于 Python 开发、Markdown 编辑等：

* **Python**：提供 Python 语法高亮、自动补全、调试等功能。
* **Pylance**：提供更快的 IntelliSense 和类型检查。
* **Jupyter**：支持 Jupyter Notebook 的编辑和运行。
* **Markdown All in One**：增强 Markdown 编辑体验。
* **GitLens**：增强 Git 功能。([apifox][1])

安装方法：

1. 打开 VSCode。
2. 点击左侧活动栏的扩展图标（或按 `Ctrl+Shift+X`）。
3. 在搜索框中输入插件名称，点击“安装”按钮。([apifox][1])

---

你

[1]: https://apifox.com/apiskills/install-vscode/?utm_source=chatgpt.com "2025年VSCode 安装下载教程（Mac & Windows & Linux）"
[2]: https://www.cnblogs.com/kyle-7Qc/p/18537085?utm_source=chatgpt.com "Python 基础知识之安装.基本使用"
[3]: https://blog.csdn.net/weixin_46904245/article/details/139407758?utm_source=chatgpt.com "Python安装步骤原创"
[4]: https://www.cnblogs.com/jzcn/p/16733969.html?utm_source=chatgpt.com "Python 安装- 浇筑菜鸟"
