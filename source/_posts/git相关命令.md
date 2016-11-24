---
title: git相关命令
date: 2016-10-11 16:11:00
tags: Git
categories: Git
---

1 基本的常用命令
- git add 添加到git仓库
- git commit -m "描述" 提交到本地
- git push origin master 提交到远程master分支
- git status 查看状态
- git add -f 文件名/文件路径 强制添加到仓库
- npm init -y这里的-y就是不用一步一步的提示，所有的都是yes

2 如果add过程中意外取消，再次执行命令的时候会提示locked

> 解决： 删除.git文件中以.locked结尾的文件

