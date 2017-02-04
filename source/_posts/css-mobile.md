---
title: 移动端开发注意事项
date: 2016-09-30 14:38:02
tags: 移动端
categories: css
---

### 移动端web的基础知识

		（mobile）font-size == 12px （pc）约等于

### viewport的content各个值和属性

		width=device-width, // 页面宽度=设备宽度
		initial-scale = 1.0，// 初始缩放
		maximum-scale = 1.0, // 最大缩放
		user-scalable  = no // 用户是否能缩放

### 字体大小设置

> 移动端页面字体大小原理：
设计图字体大小/设计图宽度 = 移动端字体大小/移动设备宽度


做法：

在入口文件中 设置移动设备根字体大小：document.documentElement.style.fontSize = window.innerWidth + "px";// 例如320px

mixin里进行字体转换：

设计图中字体大小/1080设计图宽度 * 根字体大小（1rem）无论设备的宽度是多少px，都是1rem


$pxValue/ $designFont-Size * 1rem;

注意：因为html字体大小可能会影响字间距，所以要给body重置字体大小为12px

### ios兼容问题：

* 非列表要用touchend 并且要执行e.preventDefault 因为touchstart有事件穿透问题会直接点击到下个页面的某个位置

* 列表用click会有一个300s延迟解决可用fastClick或者zepto的tap


