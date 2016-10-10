---
title: node相关
date: 2016-10-10 16:49:55
tags: node
categories: node
---

### cnpm 淘宝镜像安装地址

	npm install -g cnpm --registry=https://registry.npm.taobao.org

### ruby

> 安装ruby之后自带包管理工具例如gem

### node 常用包

> 文件系统，可以对文件进行I/O操作

	require('fs')

> 系统路径模块

	require('fs')

> 返回筛选文件夹下面的所有文件

	require('glob')

> 链接到服务器/ 自动刷新浏览器功能

	require('gulp-connect')

> 显示错误报告信息

	require('gulp-notify')

> 可以阻止 gulp 插件发生错误导致进程退出并输出错误日志。

	require('gulp-plumber')

> 给css自动加前缀

	require('gulp-postcss')

> 让gulp 任务，可以相互独立，解除任务间的依赖，增强task复用

	require('run-sequence')