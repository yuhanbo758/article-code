---
创建时间: 2024-01-13 14:51
修改时间: 2024-01-13 14:55
tags:
  - python
标题: 怎么将vscode的代码同步到github，进行开源
share: "true"
---


将 VS Code 中的代码同步到 GitHub 需要几个步骤。这里假设你已经有一个 GitHub 账户，并且在你的电脑上已经安装了 Git。以下是同步代码到 GitHub 的基本步骤：

### 1. 在 GitHub 上创建一个新仓库
1. 登录你的 GitHub 账户。
2. 在右上角，点击 "+" 图标，然后选择 "New repository"。
3. 填写仓库名称，可选择是否添加描述。
4. 选择是否要将仓库设为公开或私有。
5. 可选地，你可以初始化仓库，添加 README 文件、.gitignore 或选择许可证。
6. 点击 "Create repository"。

### 2. 在本地初始化 Git 仓库
在 VS Code 中，打开你想要上传到 GitHub 的项目文件夹，然后打开终端（通常是在菜单栏中的“视图”->“终端”），执行以下命令：

```bash
git init
git add .
git commit -m "Initial commit"
```
这些命令会初始化一个新的 Git 仓库，添加所有文件，并进行首次提交。

### 3. 将本地仓库与 GitHub 仓库关联
在你的 GitHub 仓库页面，你会找到用来关联本地仓库的 URL。复制它，然后在 VS Code 的终端中执行以下命令（请替换 `<your-repository-url>` 为你的实际仓库 URL）：

```bash
git remote add origin <your-repository-url>
git branch -M main
git push -u origin main
```

这些命令将本地仓库关联到 GitHub 上的仓库，并将代码推送到 GitHub。

### 4. 今后的同步
在未来，每当你完成代码更改并希望同步到 GitHub 时，只需执行以下命令：

```bash
git add .
git commit -m "Your commit message"
git push
```

这些命令将新更改添加到本地 Git 仓库，创建一个新的提交，并将这些更改推送到 GitHub。

### 注意事项
- 确保你在本地仓库的根目录下执行这些命令。
- 提交信息应该是描述性的，让其他人知道你做了什么更改。
- 如果你的 GitHub 仓库不是空的（例如，如果你初始化时添加了 README），你可能需要先拉取远程仓库的内容，使用命令 `git pull origin main`。

如果你还没有在电脑上配置 Git，你需要先设置你的 Git 用户名和邮箱：

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

这些是将 VS Code 中的代码同步到 GitHub 的基本步骤。如果你在操作过程中遇到任何问题，可以查阅 Git 和 GitHub 的官方文档，或者在社区寻求帮助。

