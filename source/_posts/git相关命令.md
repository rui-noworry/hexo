---
title: git相关命令
date: 2016-10-11 16:11:00
tags: Git
categories: Git
---
git 地址 https://github.com/rui-noworry

### 基本的常用命令
```bash
    - git init  在文件目录下初始化git
    - git add 添加到git仓库
    - git commit -m "描述" 提交到本地
    - git push origin master 提交到远程master分支
    - git status 查看状态
    - git add -f 文件名/文件路径 强制添加到仓库
    - npm init -y这里的-y就是不用一步一步的提示，所有的都是yes
    - git diff read.txt 查看修改了那些内容
    - git log 查看git的提交历史
    - git reset --hard HEAD^ 回退到上一个版本
      git reset --hard HEAD^^ 回退到上上个版本
      git reset --hard HEAD~100
      git reset --hard 版本号   通过版本号回退到哪个版本
    - cat read.txt  查看文件
    - git reflog  查看提交的版本号
    - git checkout -- read.txt
      两种情况下使用：
      1. readme.txt自动修改后，还没有放到暂存区，使用 撤销修改就回到和版本库一模一样的状态。
      2. 另外一种是readme.txt已经放入暂存区了，接着又作了修改，撤销修改就回到添加暂存区后的状态
    - git merge dev(当前在master分支 合并 dev分支的内容) 然后执行 git push 即生效（成功）

```



2 如果add过程中意外取消，再次执行命令的时候会提示locked

> 解决： 删除.git文件中以.locked结尾的文件

3. 更新的时候如何出现了 git rebase --continue如果一直闪动的continue

   执行 git status -> git rebase --abort -> git pull -r -> git push

4. 安装指定版本

   例如：git install vue-router@2.7.0

#### 分支命令相关总结

   总结创建与合并分支命令如下：

   查看分支：git branch

   创建分支：git branch name

   切换分支：git checkout name

   创建+切换分支：git checkout –b name

   合并某分支到当前分支：git merge name (合并后 分支的信息会消失)
                     git merge --no-ff -m '合并分支' dev (合并分支并保留 分支在 git log 的信息)

   删除分支：git branch –d name

   测试先有本地分支 然后远程创建 repository 再关联

   1. 创建本地分支： git init

      此时可以 git add 和commit

   2.远程创建分支，根据提示关联本地分支

   3.在本地分支上根据提示进行操作即可

5. 要查看远程库的信息 使用 git remote
   要查看远程库的详细信息 使用 git remote –v

### Git基本常用命令如下：

> mkdir：         XX (创建一个空目录 XX指目录名)

   pwd：          显示当前目录的路径。

   git init          把当前的目录变成可以管理的git仓库，生成隐藏.git文件。

   git add XX       把xx文件添加到暂存区去。

   git commit –m “XX”  提交文件 –m 后面的是注释。

   git status        查看仓库状态

   git diff  XX      查看XX文件修改了那些内容

   git log          查看历史记录

   git reset  –hard HEAD^ 或者 git reset  –hard HEAD~ 回退到上一个版本

                        (如果想回退到100个版本，使用git reset –hard HEAD~100 )

   cat XX         查看XX文件内容

   git reflog       查看历史记录的版本号id

   git checkout — XX  把XX文件在工作区的修改全部撤销。

   git rm XX          删除XX文件

   git remote add origin https://github.com/tugenhua0707/testgit 关联一个远程库

   git push –u(第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库

   git clone https://github.com/tugenhua0707/testgit  从远程库中克隆

   git checkout –b dev  创建dev分支 并切换到dev分支上

   git branch  查看当前所有的分支

   git checkout master 切换回master分支

   git merge dev    在当前的分支上合并dev分支

   git branch –d dev 删除dev分支

   git branch name  创建分支

   git stash 把当前的工作隐藏起来 等以后恢复现场后继续工作

   git stash list 查看所有被隐藏的文件列表

   git stash apply 恢复被隐藏的文件，但是内容不删除

   git stash drop 删除文件

   git stash pop 恢复文件的同时 也删除文件

   git remote 查看远程库的信息

   git remote –v 查看远程库的详细信息

   git push origin master  Git会把master分支推送到远程库对应的远程分支上



很好的git 学习资料：http://www.open-open.com/lib/view/open1414396787325.html
