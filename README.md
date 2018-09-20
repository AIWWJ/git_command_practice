# Git 操作

标签（空格分隔）： Git

---

**Git管理的是修改**

初始化配置：
`git config --global user.name "Your Name"`
`git config --global user.email "email@example.com"`
`git config --list0` 查看配置信息
`git cinfig <key>` 查看某一配置的信息

获取帮助：
`git help <verb>` 查看某一命令下的使用手册

##create a new repository on the command line##
`echo "# git_command_practice" >> README.md`
`git init`
`git add README.md`
`git commit -m "first commit"`
`git remote add origin` `git@github.com:AIWWJ/git_command_practice.git`
`git push -u origin master`

创建版本库：
`git init ` 初始化版本库

创建并切换分支：
`git checkout -b name ` 创建并切换到对应分支
`git checkout branchName` 切换分支
`git branch` 查看分支

提交修改：
`git status` 查看修改了哪些文件
`git diff fileName` 查看具体的修改内容
`git diff HEAD -- fileName` 查看工作区和版本库里最新版本的区别
`git add .` 提交所有修改
`git commit -m` "备注信息" 提交改动到本地git仓库
`git push origin branchName`  将本地仓库中的分支推送到远程仓库

删除分支：
`git branch -a`  查看本地和远程的分支
`git branch -d branchName` 删除本地分支
`git branch -D branchName` 强制删除本地分支
`git push origin --delete branchName` 删除远程分支

版本回退：
`git reset --hard HEAD^(或commit_id)` 回退会上一版本
在Git中，用 `HEAD` 表示当前版本，上一个版本就是 `HEAD^`，上上一个版本就是 `HEAD^^` ，往上100个版本写成 `HEAD~100` 。
`git checkout -- fileName` 丢弃工作区的修改
`git reset HEAD fileName` 可以把撤销暂存区的修改，重新放回工作区

合并（最后的2个）提交：
`git rebase -i HEAD~2`
按 `Insert` ,将第二个 `pick` 改为 `squash` 或 `s` ,按 `ESC`， 之后按 `shiift + :`  然后输入 `wq` 即可退出
此时git会自动将第二个提交合并到第一个中，按 `Insert`  然后输入新的message，按 `ESC`， 之后按 `shiift + :`  然后输入 `wq` 即可退出
通过 git log 可查看到最后的两个提交已被合并成一个
`git push --force origin branchName` 将合并之后的分支提交到远程

`git log` 查看最近到最远的提交(可加上 `--pretty=oneline` 参数过滤日志信息)，按 `Q` 可退出
`git reflog` 记录每一次命令


我们有时会遇到这样的情况，正在dev分支开发新功能，做到一半时有人过来反馈一个bug，让马上解决，但是新功能做到了一半你又不想提交，这时就可以使用 `git stash` 命令先把当前进度保存起来，然后切换到另一个分支去修改bug，修改完提交后，再切回dev分支，使用 `git stash pop` 来恢复之前的进度继续开发新功能

`git stash save 'message...'` 可以添加一些注释


把文件往Git版本库里添加的时候，是分两步执行的：
第一步是用 `git add` 把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用 `git commit` 提交更改，实际上就是把暂存区的所有内容提交到当前分支。
(需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改)
`git add` 命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行 `git commit` 就可以一次性把暂存区的所有修改提交到分支。

`git rm` 删除文件 然后`git commit`

查看系统config：
`git config --system --list`

查看当前用户（global）配置：
`git config --global  --list`

查看当前仓库配置信息：
`git config --local  --list`


1、Git 警告 `LF will be replaced by CRLF`
`rm -rf .git`  // 删除.git  
`git config --global core.autocrlf false`  //禁用自动转换    
`git init `   
`git add .`
重点是这句： `git config core.autocrlf false`


2、merge到master时有冲突（master分支上有已经被修改的同一文件）
切换到master分支： `git checkout master`
将remote master同步到local master： `git pull origin master`
切换到的local开发分支： `git checkout dev_xxx`
合并 local master 到 local的开发分支： `git merge master`
推送更新到gitlab，使gitlab同步更新显示： `git push origin feature/xxx`
(https://www.cnblogs.com/lyy-totoro/p/6889245.html)[]

关联本地和远程分支：
`git branch --set-upstream-to origin/远程分支名 本地分支名 `
`git branch --set-upstream-to=origin/remote_branch  your_branch`
其中，`origin/remote_branch` 是你本地分支对应的远程分支；`your_branch` 是你当前的本地分支。
git checkout (master分支的hash)061385a4fbcc86c0b2c6e1cccb8624bcf947bc53 _app.js(要修改的文件)
(写明文件的路径或者进入对应的文件夹下)

3、查看某一行代码的修改历史
`git blame fileName` 其显示格式为： 
commit ID | 代码提交作者 | 提交时间 | 代码位于文件中的行数 | 实际代码 
然后通过 `git show commitID` 查看