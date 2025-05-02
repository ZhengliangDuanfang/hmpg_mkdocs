# Git笔记

## 本地操作

- `git init` 初始化一个本地仓库
- `git add .` 添加所有文件到暂存区
- `git commit -m "message"` 提交暂存区的文件到本地仓库
- `git status` 查看当前状态

### 分支操作

- `git branch` 查看分支
- `git branch <branch-name>` 创建分支
- `git checkout <branch-name>` 切换分支
- `git checkout -b <branch-name>` 创建并切换分支

- `git merge <branch-name>` 将其他分支合并进当前分支
- `git branch -d <branch-name>` 删除分支

### 查看历史

- `git log` 查看提交历史
- `git log --oneline` 查看简洁的提交历史
- `git log --graph` 查看分支合并情况
- `git log --all` 显示其它分支的信息

### 回退

- `git reset --hard <commit-id>` 回退到`commit-id`对应的版本，添加到暂存区但是没有提交到本地仓库的内容以及没有存入暂存区的内容全部彻底消失。`commit-id`可以用`git log`相关指令查看。

## 远程仓库

- `git clone <repo-url>` 克隆远程仓库
- `git clone <repo-url> <local-directory-name>` 克隆远程仓库到指定目录

如果报错没有权限，需要配置SSH key。参考[CSDN](https://blog.csdn.net/weixin_42310154/article/details/118340458)。
注意这种方法在后续克隆的时候要采用SSH的方式，而不是直接输入仓库HTTPS地址。

- `git remote add <origin-name> <repo-url>` 添加远程仓库地址
    - `<origin-name>` 一般为`origin`，如果有多个远程仓库，可以取其他名字
- `git remote -v` 查看远程仓库地址
- `git push <origin-name> <branch-name>` 推送本地仓库到远程仓库
    - 第一次推送，需要加上`-u`参数，即`git push -u <origin-name> <branch-name>`
    - 如果想要本地与远程分支名称不同，可以`git push <remote> <local-branch>:<remote-branch>`

- `git pull <origin-name> <branch-name>` 拉取远程分支到本地
- `git fetch <origin-name> <branch-name>` 从远程仓库拉取最新的分支，但不合并
- `git checkout -b <new-branch-name> <origin-name>/<branch-name>` 将远程分支拉取到本地并创建一个新的分支
  
### deploy key

!!! TODO
    [https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/managing-deploy-keys#deploy-keys](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/managing-deploy-keys#deploy-keys)