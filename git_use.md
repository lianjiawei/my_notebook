# Git 入门使用教程

## 1. Git 简介

### 什么是 Git

Git 是一个**分布式版本控制系统**，用于跟踪文件的修改历史。每个开发者的本地仓库都包含完整的版本记录，无需依赖中央服务器即可独立工作。

### 为什么要使用 Git

- **版本管理**：随时回退到任意历史版本，不再需要手动备份文件
- **多人协作**：多人可以同时修改同一个项目，Git 负责合并变更
- **分支开发**：可以创建独立分支进行实验性开发，不影响主线代码
- **开源生态**：GitHub、GitLab 等平台基于 Git，是参与开源项目的基础

---

## 2. Git 安装与验证

### 各平台安装方式

**Windows：**

前往 [Git 官网](https://git-scm.com/download/win) 下载安装包，按默认选项完成安装。

**macOS：**

```bash
# 使用 Homebrew 安装
brew install git
```

**Linux（Debian/Ubuntu）：**

```bash
sudo apt update
sudo apt install git
```

**Linux（CentOS/Fedora）：**

```bash
sudo yum install git
# 或
sudo dnf install git
```

### 安装验证

安装完成后，打开终端执行以下命令确认安装成功：

```bash
git --version
```

输出类似 `git version 2.43.0` 即表示安装成功。

### 常见安装问题排查

- **提示 `git` 不是可识别的命令**：检查 Git 是否已添加到系统环境变量 `PATH` 中
- **Windows 用户**：安装时建议勾选 "Git Bash Here"，方便在任意目录打开终端
- **权限问题**：Linux/macOS 下使用 `sudo` 执行安装命令

---

## 3. Git 基础配置与检查

### 用户名和邮箱配置

首次使用 Git 前，必须设置用户名和邮箱（会记录在每次提交中）：

```bash
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱@example.com"
```

### 查看当前配置

```bash
# 查看所有配置
git config --list

# 只查看全局配置
git config --global --list

# 查看单项配置
git config user.name
git config user.email
```

### 配置文件位置

| 级别 | 位置 | 说明 |
|------|------|------|
| 系统级 | `/etc/gitconfig` | 对所有用户生效 |
| 全局级 | `~/.gitconfig` | 对当前用户生效 |
| 仓库级 | `.git/config` | 仅对当前仓库生效 |

优先级：仓库级 > 全局级 > 系统级

### 其他常用配置

```bash
# 设置默认编辑器为 VS Code
git config --global core.editor "code --wait"

# 设置默认分支名为 main
git config --global init.defaultBranch main

# Windows 用户建议设置换行符自动转换
git config --global core.autocrlf true

# macOS/Linux 用户建议设置
git config --global core.autocrlf input
```

---

## 4. GitHub 介绍与基本操作

### GitHub 是什么

GitHub 是全球最大的基于 Git 的**代码托管平台**，提供远程仓库托管、协作开发、项目管理等功能。

### 注册账号与创建仓库

1. 访问 [github.com](https://github.com) 注册账号
2. 点击右上角 **"+"** → **"New repository"** 创建新仓库
3. 填写仓库名称，选择公开/私有，点击 **"Create repository"**

### SSH 密钥配置

使用 SSH 可以免密码推送代码：

```bash
# 1. 生成 SSH 密钥
ssh-keygen -t ed25519 -C "你的邮箱@example.com"

# 2. 查看公钥内容
cat ~/.ssh/id_ed25519.pub
```

3. 将公钥内容复制到 GitHub：**Settings** → **SSH and GPG keys** → **New SSH key**

```bash
# 4. 测试连接
ssh -T git@github.com
```

输出 `Hi 用户名! You've successfully authenticated` 即表示配置成功。

### 将本地仓库关联到 GitHub

```bash
# 在已有的本地仓库中添加远程地址
git remote add origin git@github.com:用户名/仓库名.git

# 首次推送并设置上游分支
git push -u origin main
```

### Fork 与 Pull Request

- **Fork**：将别人的仓库复制一份到自己的账号下，可以自由修改
- **Pull Request (PR)**：修改完成后向原仓库提交合并请求，由维护者审核后合并

基本流程：Fork → Clone → 修改 → Push → 发起 Pull Request

### GitHub 常用页面功能

| 功能 | 说明 |
|------|------|
| **Code** | 浏览仓库代码和文件 |
| **Issues** | 提交 Bug 报告或功能建议 |
| **Pull Requests** | 查看和管理合并请求 |
| **Actions** | CI/CD 自动化工作流 |
| **Releases** | 发布版本和下载包 |
| **Wiki** | 项目文档 |

---

## 5. 核心概念

Git 管理文件有三个区域：

```
工作区 (Working Directory)
  │
  │  git add
  ▼
暂存区 (Staging Area)
  │
  │  git commit
  ▼
本地仓库 (Repository)
  │
  │  git push
  ▼
远程仓库 (Remote)
```

- **工作区**：你实际编辑文件的目录
- **暂存区**：已标记为下次提交内容的区域（通过 `git add` 添加）
- **本地仓库**：已提交的完整版本记录（通过 `git commit` 保存）
- **远程仓库**：托管在服务器上的仓库（通过 `git push` 同步）

---

## 6. 常用命令

### 6.1 仓库操作

**初始化新仓库：**

```bash
git init
```

在当前目录创建一个新的 Git 仓库。

**克隆远程仓库：**

```bash
# 使用 HTTPS
git clone https://github.com/用户名/仓库名.git

# 使用 SSH
git clone git@github.com:用户名/仓库名.git

# 克隆到指定目录
git clone https://github.com/用户名/仓库名.git 目标目录名
```

### 6.2 文件操作

**添加文件到暂存区：**

```bash
# 添加单个文件
git add 文件名

# 添加所有修改过的文件
git add .

# 添加指定类型的文件
git add *.py
```

**删除文件：**

```bash
# 从仓库和工作区同时删除
git rm 文件名

# 仅从仓库删除，保留本地文件
git rm --cached 文件名
```

**重命名/移动文件：**

```bash
git mv 旧文件名 新文件名
```

### 6.3 提交操作

**查看当前状态：**

```bash
git status
```

**查看修改内容：**

```bash
# 查看工作区与暂存区的差异
git diff

# 查看暂存区与最新提交的差异
git diff --cached

# 查看两个分支的差异
git diff 分支1 分支2
```

**提交更改：**

```bash
# 提交暂存区的内容
git commit -m "提交说明"

# 跳过 git add，直接提交所有已跟踪文件的修改
git commit -am "提交说明"
```

### 6.4 分支操作

**查看分支：**

```bash
# 查看本地分支
git branch

# 查看所有分支（包括远程）
git branch -a
```

**创建分支：**

```bash
# 创建新分支
git branch 分支名

# 创建并切换到新分支
git checkout -b 分支名
# 或（推荐）
git switch -c 分支名
```

**切换分支：**

```bash
git checkout 分支名
# 或（推荐）
git switch 分支名
```

**合并分支：**

```bash
# 将指定分支合并到当前分支
git merge 分支名
```

**删除分支：**

```bash
# 删除已合并的分支
git branch -d 分支名

# 强制删除未合并的分支
git branch -D 分支名
```

### 6.5 远程操作

**管理远程仓库：**

```bash
# 查看远程仓库
git remote -v

# 添加远程仓库
git remote add origin 远程仓库地址

# 修改远程仓库地址
git remote set-url origin 新地址
```

**推送代码：**

```bash
# 推送到远程分支
git push origin 分支名

# 首次推送并设置上游分支
git push -u origin 分支名

# 已设置上游后可以简写
git push
```

> **`-u` 参数说明：** `-u` 是 `--set-upstream` 的简写，作用是将本地分支与远程分支建立跟踪关系。只需要在新分支**首次推送时使用一次**，之后 Git 会记住对应关系，后续 `git push` 和 `git pull` 就不需要再指定 `origin 分支名` 了。可以用 `git branch -vv` 查看当前的跟踪关系。

**拉取代码：**

```bash
# 拉取并合并（等于 fetch + merge）
git pull

# 拉取指定远程分支
git pull origin 分支名
```

**获取远程更新（不合并）：**

```bash
git fetch

# 获取指定远程仓库的更新
git fetch origin
```

### 6.6 查看历史

**查看提交日志：**

```bash
# 查看完整日志
git log

# 单行显示
git log --oneline

# 显示分支图
git log --oneline --graph --all

# 查看最近 N 条
git log -5
```

**查看操作记录：**

```bash
# 查看所有 HEAD 变动记录（包括已回退的提交）
git reflog
```

### 6.7 撤销与回退

**恢复工作区文件：**

```bash
# 撤销工作区的修改（恢复到暂存区或最新提交的状态）
git restore 文件名

# 取消暂存（从暂存区移回工作区）
git restore --staged 文件名
```

**回退提交：**

```bash
# 软回退：撤销提交，保留修改在暂存区
git reset --soft HEAD~1

# 混合回退（默认）：撤销提交，保留修改在工作区
git reset HEAD~1

# 硬回退：撤销提交，丢弃所有修改（慎用）
git reset --hard HEAD~1
```

**创建反向提交（安全的撤销方式）：**

```bash
# 创建一个新提交来撤销指定提交的更改
git revert 提交哈希
```

### 6.8 暂存工作

当你需要临时切换分支但不想提交当前修改时：

```bash
# 暂存当前修改
git stash

# 暂存并添加说明
git stash push -m "说明信息"

# 查看暂存列表
git stash list

# 恢复最近一次暂存（保留暂存记录）
git stash apply

# 恢复最近一次暂存（删除暂存记录）
git stash pop

# 删除所有暂存
git stash clear
```

### 6.9 标签管理

```bash
# 创建轻量标签
git tag v1.0.0

# 创建附注标签（推荐）
git tag -a v1.0.0 -m "发布 1.0.0 版本"

# 查看所有标签
git tag

# 推送标签到远程
git push origin v1.0.0

# 推送所有标签
git push origin --tags

# 删除本地标签
git tag -d v1.0.0

# 删除远程标签
git push origin --delete v1.0.0
```

---

## 7. 常见场景速查

### 场景一：从零开始一个新项目

```bash
mkdir my-project && cd my-project
git init
echo "# My Project" > README.md
git add .
git commit -m "初始化项目"
git remote add origin git@github.com:用户名/仓库名.git
git push -u origin main
```

### 场景二：参与已有项目

```bash
git clone git@github.com:用户名/仓库名.git
cd 仓库名
# 创建功能分支
git switch -c feature/新功能
# 编辑文件...
git add .
git commit -m "添加新功能"
git push -u origin feature/新功能
# 然后在 GitHub 上创建 Pull Request
```

### 场景三：同步上游仓库（Fork 的项目）

```bash
# 添加上游仓库
git remote add upstream git@github.com:原作者/仓库名.git
# 获取上游更新
git fetch upstream
# 合并到本地 main 分支
git switch main
git merge upstream/main
# 推送到自己的远程仓库
git push origin main
```

### 场景四：解决合并冲突

```bash
git merge feature/分支名
# 如果出现冲突，手动编辑冲突文件
# 冲突标记格式：
# <<<<<<< HEAD
# 当前分支的内容
# =======
# 合并分支的内容
# >>>>>>> feature/分支名

# 解决冲突后
git add .
git commit -m "解决合并冲突"
```

### 场景五：误提交后回退

```bash
# 撤销最近一次提交，保留修改
git reset --soft HEAD~1

# 修改后重新提交
git add .
git commit -m "修正后的提交"
```
