---
title: position各个值的用法
date: 2016-09-29 18:00:59
tags: css
categories: css
---

### absolute

> 给对象设置了absolute原来的位置消失 不设置left，top，会自动跑到父层的左上角 设置left，top 以body为基准点 给对象父层设置relative或者有abosolute，就会基于他最近的position移动

### relative

> 原来的位置还在，基于本身移动，父层设置position什么都与他无关

### fixed（ie6不支持）

> 以body为基准点， 原来的位置消失 父层设置position什么都与他无关 不设置left，top，会自动跑到父层的左上角 设置left，top 以body为基准点


