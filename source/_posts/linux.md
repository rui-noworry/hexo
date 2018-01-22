---
title: linux常用命令
date: 2018-01-22 16:39:57
tags: linux
categories: linux
---

### linux常用操作

> 复制文件目录到另一个目录（目标文件不存在，如何存在则将整个目录复制进去）：

``` bash
 cp -a static static1
```

> 复制文件下的所有内容到另一个文件夹并覆盖里面的所有文件：

``` bash
 \cp calculator/* -r -a calculator-clone
```

> 删除文件夹：

rm -rf 文件名
-r 就是向下递归，不管有多少级目录，一并删除
-f 就是直接强行删除，不作任何提示的意思

> 创建文件夹：

mkdir 文件名
如何删除github上的某一个目录
