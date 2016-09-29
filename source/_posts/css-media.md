---
title: css响应式
date: 2016-09-29 18:19:17
tags: css
categories: css
---

> * media querie（@media）允许在不改变内容的情况下，改变布局以适应不同设备浏览器情况
* 关键字：not and only screen 媒体类型 min-width媒体特性

1. 在link中写法


		<link rel=”stylesheet” type=”text/css” href=”styleA.css” media=”screen and (min-width:400px)” />

		<link rel=”stylesheet” type=”text/css” href=”styleA.css” media=”screen and (min-width:400px) and (max-width=800px)” />

		<link rel=”stylesheet” type=”text/css” href=”styleA.css” media=”only screen and (-webkit-min-device-pixel-ratio:2)” />

2. 在css中写法


		@media only screen and (min-width=1024px){ .content{ width:1000px; martin:auto} }
		@media only screen and (min-width=400px) and (max-width=1024px){
			 .right{
				width:0px
			}
			.left{
				width:30%
			}
			.right{
				width:65%
			} }
		@media only screen and (max-width=400px) {
			 .right,.left,.right{
				width:98%; height:200px
			} }

3. hack ie9以下不支持 就加这个 js引用

		<script src=http://css3-mediaqueries-js.googlecode.com/svn/trunk/css3-mediaqueries.js></script>

``` bash
	注意事项：
	头部一定要加： <meta content:”width=device-width,initial-scale=1” name=”viewport” />
	Html{font-size:62.5%; }初始化字体为10px（1rem=10px便于计算）例如:body{font-size:20px; font-size:2rem;}
	一定要设置max-width/min-width
	Box-sizzing:border-box;
```
