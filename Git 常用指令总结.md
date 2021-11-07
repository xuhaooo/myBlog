# Git 常用指令总结

# 一、全局配置

```bash
# 设置全局的 git 用户姓名、提交者邮箱
git config --global user.name yourname 
git config --global user.email youremail
```

由于 Git 是分布式版本控制系统，所以每个机器得自报家门

```bash
# 查看所有的 config 信息
git config --list
```

配置的优先级为：`git config > git config --global > git confing -—system`

使用了 `--global` 这个参数表示你的机器上所有的仓库都会使用这个配置，当然也可以指定某个仓库的配置

# 二、本地操作

## 1. 创建版本库

```bash
# cd somedir
git init
```

版本库又称仓库、repository，在版本库中的所有文件、操作都会被 Git 管理追踪

这个命令会将目录变成 Git 可以管理的仓库，同时会在目录中创建一个 `.git` 目录，用来追踪管理版本库

## 2. 添加文件到版本库

```bash
# 添加新文件
git add newfile
# 添加修改文件
git add modify-file
# 添加所有文件
git add .
# 添加某个后缀的所有文件
git add *.txt
```

## 3. 提交文件到版本库

```bash
# 提交更新
git commit -m "提交描述信息"
```

## 4. 查看版本库状态

```bash
# 查看工作区当前状态
git status
# 查看工作区与暂存区的差异，即尚未添加暂存的改动
# - 表示改动前，+ 表示改动后
git diff
# 查看暂存区与版本库的差异，即已经暂存的改动
git diff --cached
# 查看某文件工作区与版本库最新版本的差异
git diff HEAD -- filename
```

## 5. 查看提交/命令历史

```bash
# 列出所有提交记录
git log
# 列出提交的简略信息
git log --pretty=oneline
# 列出分支合并图
git log --graph (--pretty=oneline (--abbrev-commit))
```

可以看到 commit id 以及 HEAD 指向

```bash
# 查看每一次命令
git reflog
```

## 6. 版本回退

```bash
# 回退的上一个、上上个、指定的版本
git reset --hard HEAD^/HEAD^^/commit id
```

## 7. 撤销操作

```bash
# 撤销工作区的修改，让文件回到最近一次 git add 或 git commit 的状态
# 如果没有暂存就撤销掉所有修改，如果暂存后修改就撤销惠回到暂存后的状态
git checkout -- filePath
# 把暂存区的修改撤销到工作区
git reset HEAD filePath
```

## 8. 创建分支

```bash
# 创建 newb 分支，并切换到 newb 分支
git checkout -b newb
# -b 表示创建并切换，等价于
git branch newb
git checkout newb

# 查看当前分支
git branch

# 切换分支
git checkout branchName
```

未创建分之前，Git 默认是将 HEAD 指针指向 master 主分支指针，而 master 指向最新的提交

创建分支之后，Git 会将 HEAD  指针指向新创建的分支指针比如 newb，而 newb 会指向与 master 相同的提交

## 9. 合并、删除分支

```bash
# git merge 用于合并指定分支到当前分支
# 合并 newb 分支到 master 分支
git checkout master
git merge newb

# 使用 --no-ff 参数，不使用 fast-forward 合并，保留合并历史
git merge --no-ff -m "合并描述信息" newb

# 删除指定分支
git branch -d branchName
# 未合并的分支，强行删除
git branch -D branchName
```

## 10. 将工作现场暂时移除“储藏”

```bash
# 暂时将未提交的的工作现场移除，储藏起来
git stash
# 查看储藏起来的工作现场
git stash list

# 恢复工作现场但不删除 stash 内容
git stash apply
# 恢复指定的 stash 内容
git stash apply stash@{number}
# 删除 stash 内容
git stash drop

# 恢复工作现场同时删除 stash 内容
git stash pop
```

## 11. 复制特定的提交到当前分支

```bash
git cherry-pick [commit id]
```

多个分支上的相同 bug 修复，提交之后，可以通过这一操作，在多个分支上重放

## 12. 标签管理

tag 就是一个让人容易记住的有意义的名字，它与某个 commit 绑定

如果某个 commit 在多个分支上都有，那么多个分支上都能看到这个 tag 

```bash
# 打标签
git tag tagName
# 指定给某次提交打标签（默认是打在最新的提交上）
git tag tagName [commit id]

# -a 指定标签名，-m 指定说明文字
git tag -a tagName -m "tag discription" [commit id]

# 查看所有标签
git tag
# 查看标签信息
git show tagName

# 推送一个本地标签到远程
git push origin tagName
# 推送全部未推送的标签到远程
git push origin --tags

# 删除本地标签
git tag -d tagName
# 删除远程标签
git push origin :refs/tags/tagName
```

## 13. 远程仓库管理

```bash
# 将本地仓库与远程仓库 origin 关联，远程库的名字默认是 origin
git remote add origin git@github.com:用户名/仓库名
# 添加多个远程仓库的关联
git remote add gitee gitee@gitee.com:用户名/仓库

# -u 参数是因为，第一次推送时远程仓库 orgin 是空的
# 而且将本地 master 分支与远程 master 分支关联，并把内容推送过去
git push -u origin master
# 之后就可以简化，将本地 master 最新提交推送到远程仓库
git push
git push gitee master

# 查看远程库信息
git remote -v

# 删除远程库，删除的意思是解除本地与远程的绑定关系
git remote rm origin

# 克隆远程仓库到本地
# 实际上，Git 将本地仓库与远程仓库的 master 分支关联起来，默认只能看到本地的 master 分支
git clone 仓库链接

# 将远程新建的分支拉到本地
git checkout -b <branch-name> origin/<branch-name>

# 本地新建分支，将本地指定分支推送到远程指定分支（前面的是本地指定分支，后面的是远程指定分支）
git checkout -b <branch-name>
git push origin <branch-name>:<branch-name>

# 建立本地分支、远程分支的链接关系
git branch --set-upstream <branch-name> origin/<branch-name>

# 防止远程有更新，先拉再推
git pull
git push 

# 将远程主机的最新内容拉下来后直接合并，相当于 git fetch + git merge
git pull
# 将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中
git fetch

# 多人协作
# 推送自己的修改
git push origin <branch-name> 
# 推送失败则远程有更新，要合并
git pull
# 拉取失败，可能是因为本地分支、远程分支没有连接
git branch --set-upstream <branch-name> origin/<branch-name>
# 拉取合并成功则可以解决代码冲突或提交本地修改了
```