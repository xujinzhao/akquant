# 贡献源代码

## 环境搭建

### 安装依赖

   - 克隆项目到本地后，进入项目目录。
   - 运行以下命令安装项目依赖：

     ```shell
     pip install -r requirements.txt
     ```

### 安装 pre-commit 和 ruff

   - 项目使用 pre-commit 进行代码风格检查和格式化，使用 ruff 进行代码质量检查。
   - 运行以下命令安装 pre-commit 和 ruff：

     ```shell
     pip install pre-commit ruff
     ```

   - 在项目根目录下运行以下命令安装 pre-commit 的 Git 钩子：
     ```shell
     pre-commit install
     ```

## 贡献流程

### Fork 项目

   - 访问 akfamily/akquant 项目的 GitHub 主页：https://github.com/akfamily/akquant
   - 点击页面右上角的 "Fork" 按钮。
   - GitHub 会将项目复制到您自己的账户下，创建一个您可以编辑的副本。

### Clone 项目到本地

   - 在您的 GitHub 账户下，进入刚刚 fork 的 akquant 项目。
   - 点击 "Code" 按钮，复制项目的 HTTPS 或 SSH 地址。
   - 打开终端，导航到您想要存放项目的本地目录。
   - 运行以下命令将项目克隆到本地：

     ```shell
     git clone https://github.com/YourUsername/akquant.git
     ```

   - 将 `YourUsername` 替换为您的 GitHub 用户名。

### 创建一个新的分支

   - 进入项目目录：

     ```shell
     cd akquant
     ```

   - 创建一个新的分支来进行您的修改：

     ```shell
     git checkout -b my-feature
     ```

   - 将 `my-feature` 替换为您要开发的功能或修复的名称。

### 进行修改并提交

   - 使用您喜欢的编辑器或 IDE 对项目进行修改或添加新功能。
   - 完成修改后，提交您的更改:

     ```shell
     git add .
     git commit -m "添加了新功能"
     ```

   - 提交信息应该简洁明了地描述您所做的更改。
   - pre-commit 会在提交时自动运行代码风格检查和格式化。

### 推送到您的 GitHub 仓库

   - 将本地的修改推送到您的 GitHub 仓库：

     ```shell
     git push origin my-feature
     ```

   - 将 `my-feature` 替换为您之前创建的分支名称。

### 创建 Pull Request

   - 在您的 akquant 项目页面上，点击 "Compare & pull request" 按钮。
   - 确保 "base repository" 是 `akfamily/akquant`，而 "head repository" 是您自己的仓库。
   - 填写 Pull Request 的标题和描述，提供关于您所做修改的详细信息。
   - 点击 "Create Pull Request" 按钮提交。

### 等待审核和合并

   - akquant 项目的维护者将审核您的 Pull Request，并可能会提供反馈或要求进一步的修改。
   - 如果需要进行更改，可以在本地进行修改。然后重复步骤 4-5，将修改推送到您的仓库。
   - 一旦您的 Pull Request 被接受并合并，您的贡献将成为 akquant 项目的一部分。

希望以上详细的步骤能为您贡献 akquant 项目提供指导。
如果您有任何其他问题，欢迎随时向项目维护者提出。祝您贡献顺利!
