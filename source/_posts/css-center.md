---
title: css居中总结
date: 2016-09-29 17:15:34
tags: css
categories: css
---

### 行内元素水平垂直居中

		text-align : center;
		vertical-align : middle;
		line-height

### 块元素水平垂直居中

> 方法 1 缺点：必须知道宽高

		position：absolute；
		width：100px；
		height:100px;
		Top:50%;
		left:50%;
		transform:translate(-50%, -50%);

> 方法 2 优点：无需知道高宽

		position：absolute；
		width：100px；
		height:100px;
		Top:50%;
		left:50%;
		margin-top:-50px;
		margin-left:-50px;

> 方法 3

		position：absolute；
		width：100px；
		height：100px;
		Top：0;
		left：0;
		right：0;
		bottom：0;
		margin：auto;
		left：50%;
		margin-top：-50px;
		margin-left：-50px;

> 方法 4
> 模拟成盒子 (针对块元素的水平垂直居中)
> 注意设置兼容性加各种前缀（mox, ms 等）
>  父层 ：

		display：-webkit-box
		-webkit-box-pack：center
		-webkit- box-align：center

> 方法 5
> 父层设置 新支持android4.4以上和ios
> 注意设置兼容性加各种前缀（mox, ms 等）
> 父层：

		display：-webkit-flex
		align-items：center
		justify-content：center
