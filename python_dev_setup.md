在进行 Python 开发时，通常会涉及以下三种工具：

1. **Python**：作为编程语言，提供了基础的语法和标准库。
2. **VSCode**：作为集成开发环境（IDE），提供代码编辑、调试和插件支持。
3. **Git**：作为版本控制工具，用于管理代码的历史和协作。

这些工具相互配合，共同构建高效的开发环境。以下是对这三者的详细介绍：

---

## 1. Python：语言与包管理

### 安装 Python

* **官网下载**：访问 [python.org](https://www.python.org/downloads/) 下载适合操作系统的安装包。
* **安装建议**：

  * 勾选 **Add Python to PATH**，以便在命令行中直接使用 `python` 和 `pip`。
  * 推荐安装 **Python 3.9** 或 **3.10** 版本，兼容性好，支持大部分库。

### 安装与更新 `pip`

`pip` 是 Python 的包管理工具，通常随 Python 一起安装。

* **更新 `pip`**：

```bash
  python -m pip install --upgrade pip
```



### 切换 `pip` 镜像源

在国内使用默认的 PyPI 镜像可能速度较慢，可以切换到国内镜像源：

* **临时使用镜像源**：

```bash
  pip install -i https://pypi.tuna.tsinghua.edu.cn/simple package_name
```



* **永久修改镜像源**：

  * **Windows**：编辑 `C:\Users\<YourUsername>\AppData\Roaming\pip\pip.ini`，添加：

    ```ini
    [global]
    index-url = https://pypi.tuna.tsinghua.edu.cn/simple
    ```

  * **Linux/macOS**：编辑 `~/.config/pip/pip.conf`，添加：

    ```ini
    [global]
    index-url = https://pypi.tuna.tsinghua.edu.cn/simple
    ```

---

## 2. VSCode：开发环境与插件支持

### 安装 VSCode

* **官网下载**：访问 [code.visualstudio.com](https://code.visualstudio.com/) 下载适合操作系统的安装包。

### 安装 Python 插件

* **Python 插件**：在 VSCode 的扩展市场中搜索并安装 `Python` 插件（由 Microsoft 提供），该插件提供语法高亮、代码补全、调试等功能。
* **Pylance 插件**：安装 `Pylance` 插件，提供更快的类型检查和智能提示。

### 配置 Python 解释器

* **选择解释器**：按 `Ctrl+Shift+P` 打开命令面板，输入 `Python: Select Interpreter`，选择对应的 Python 解释器。

### 常用 VSCode 插件

* **autoDocstring**：自动生成函数的 docstring，支持多种格式。
* **Black Formatter**：自动格式化代码，遵循 PEP 8 风格。
* **GitLens**：增强 Git 功能，查看代码历史和作者信息。
* **Jupyter**：支持 Jupyter Notebook 的编辑和运行。([Towards The Cloud][1])

---

## 3. Git：版本控制与项目管理

### 安装 Git

* **官网下载**：访问 [git-scm.com](https://git-scm.com/) 下载适合操作系统的安装包。

### 配置 Git

* **设置用户名和邮箱**：

```bash
  git config --global user.name "Your Name"
  git config --global user.email "you@example.com"
```



### 克隆 GitHub 项目

* **克隆项目**：

```bash
  git clone https://github.com/username/repo.git
```



* **进入项目目录**：

```bash
  cd repo
```



* **安装依赖**：

```bash
  pip install -r requirements.txt
```



---

## 常用 Python 库（根据开发需求选择）

### 数据科学与机器学习

* **NumPy**：提供高效的数值计算功能。
* **pandas**：数据处理和分析工具。
* **Matplotlib**：绘制静态、动态和交互式图表。
* **scikit-learn**：机器学习库，提供分类、回归、聚类等算法。
* **TensorFlow** / **PyTorch**：深度学习框架。([My Great Learning][2])

### Web 开发

* **Flask**：轻量级 Web 框架。
* **Django**：全功能 Web 框架。([en.wikipedia.org][3])

### 网络请求与数据处理

* **Requests**：简化 HTTP 请求的库。
* **BeautifulSoup**：网页解析库。
* **lxml**：高性能的 XML 和 HTML 解析库。

### 测试与调试

* **pytest**：功能强大的测试框架。
* **unittest**：Python 内置的测试框架。
* **pdb**：Python 内置的调试器。

---

通过上述工具和配置，你可以搭建一个高效的 Python 开发环境，适用于数据科学、机器学习、Web 开发等多种场景。

[1]: https://towardsthecloud.com/blog/best-vscode-extensions-python?utm_source=chatgpt.com "10 Must-Have VS Code extensions for Python developers"
[2]: https://www.mygreatlearning.com/blog/open-source-python-libraries/?utm_source=chatgpt.com "Top 30 Python Libraries To Know"
[3]: https://en.wikipedia.org/wiki/Matplotlib?utm_source=chatgpt.com "Matplotlib"
