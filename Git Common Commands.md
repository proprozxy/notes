## Git Common Commands

### 1. 配置 Git

- `git config --global user.name "<name>"`：设置全局用户名。
- `git config --global user.email "<email address>"`：设置全局邮箱地址。
- `git config --list`：列出所有 Git 配置。

### 2. 初始化和克隆仓库

- `git init`：在现有目录中初始化新的 Git 仓库。
- `git clone <repository URL>`：克隆（复制）一个现有的 Git 仓库。

### 3. 基础操作

- `git add <file>`：将文件更改添加到暂存区。
- `git status`：查看工作区和暂存区状态。
- `git commit -m "<commit message>"`：将暂存区的更改提交到仓库历史中。
- `git log`：查看提交历史。

### 4. 分支管理

- `git branch`：列出所有本地分支。
- `git branch <branch name>`：创建新分支。
- `git checkout <branch name>`：切换到指定分支。
- `git merge <branch name>`：将指定分支合并到当前分支。
- `git branch -d <branch name>`：删除分支。

### 5. 远程仓库操作

- `git remote add <remote name> <repository URL>`：添加新的远程仓库。
- `git fetch <remote name>`：从远程仓库下载新分支和数据。
- `git pull <remote name> <branch name>`：从远程仓库抓取并合并到当前分支。
- `git push <remote name> <branch name>`：上传本地分支到远程仓库。

### 6. 撤销更改

- `git checkout -- <file>`：撤销对文件的未暂存的更改。
- `git reset HEAD <file>`：从暂存区撤销对文件的更改。
- `git revert <commit>`：生成一个新的提交，这个提交会撤销指定的提交所做的所有更改。
- `git reset --hard <commit>`：重置当前分支的HEAD到指定提交，同时重置工作区和暂存区，**慎用**。

### 7. 标签管理

- `git tag`：列出所有标签。
- `git tag <tag name>`：基于当前提交创建一个新的轻量标签。
- `git tag -a <tag name> -m "<tag message>"`：创建一个带有说明的标签。

### 8. 高级操作

- `git stash`：临时存储未提交的更改，以便清理工作区。
- `git stash pop`：应用存储的更改回工作区。
- `git cherry-pick <commit>`：将其他分支的提交应用到当前分支。
- `git rebase <base branch>`：将当前分支的更改重新应用到基底分支上。