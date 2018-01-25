---
title: eclips安装配置以及项目导入
date: 2018-01-25 11:13:02
tags: eclipse
categories: 工具安装配置
---

### 安装：jdk：jdk-7u80-windows-x64 （记住安装路径，要配置环境变量）

* 配置环境变量:

	在系统变量里新建：JAVA_HOME=C:\jdk1.5.0_06 后面是jdk的安装目录：例如F:\jdk

	在系统变量里新建：CLASSPATH=.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar （固定写法）

	编辑系统变量的path： 在里面新建变量 %JAVA_HOME%\bin 在新建变量：%JAVA_HOME%\jre\bin

> 在cmd命令行输入：java -version 查看是否已经成功安装

### 获取免安装的eclipse eclipse-jee-mars-2-win32-x86_64  启动

* 创建新节点项目：

 1. 新建文件夹

 2. checkout 项目

 3. fill -> switch workspace 切换工作区

 4. 左侧目录位置 右键 import->import -> Maven-> exitsed Maven Porject

 5. 添加tomcat 这个是服务（注意：添加的时候 选择jre）

   双击服务设置选项：timeout start 提高至500，publishing 选择第二项，server locations 选择第二项

   点击open launch configuratioin/arguments 在VM arguments 最后一行添加一下内容

        -Xms1024m -Xmx4096m -XX:PermSize=128M -XX:MaxPermSize=256m


** 注意： 服务配置port 端口号 然后再启动服务 **

