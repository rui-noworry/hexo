---
title: html5 新增元素介绍
date: 2016-09-30 15:26:23
tags: html
categories: html
---

### article

> 用于文章，里面可以嵌套header，footer，section评论（独立的一块内容）

### section

> 最好用于有标题的模块，或区域，若没有标题，不建议使用，（作用是最页面上的内容进行分块） 如果aside等元素更适合就不要用section元素

### aside

> (1)用于被包涵在article中主要内容的附属内容 (2)用于全局页面的附属信息


### time

> time元素代表24小时中的某个时间或者日期，表示时间的时候允许有时差
定义的格式： 2014年9月28日 9月28日 今天的时间 2014年9月28日晚上10点 UTC标准时间2014年9月28日晚上10点 中国时间2014年9月28日晚上10点

### pubdate

> 只是表示文章的发布时间

### header

> 一个网页里可以有多个header元素，不做限制

### hgroup

> 通常情况下文章只有一个主标题的时候是不需要hgroup元素的若有副标题需要使用

### footer

> 一个网页里可以有多个footer元素，不做限制，也可以用在article和section中

### address

> 是指网页中或文章中的联系信息部分（仅仅是联系信息，不要把时间等加进去）

### figurecaption

> 必须写在figure元素的内部，代表figure元素的标题

### figure

> 元素里有且只能有一个figurecaptain元素，代表原来的li标签，一般图片和标题的组合来使用，

### figurecaption放在figure元素的第一个或者最后一个位置

### details元素和summary元素

> summary元素从属于details元素，展开缩放功能，目前只有chrome浏览器支持

### mark

> 对文章内容某些文字进行突出，高亮显示，或者是用于与作者无关的某种目的的突出内 容来吸引作者的眼球

### progress

> 进度，过程，有value和max两个属性，value大于0且小于max，max必须大于0，进度可以用0-100之间的数字,显示一个默认的进度条，可以给进度条设置样式

### meter

> 有六个属性值，value，max，min，low，high，optimum

### ol

> 新增了两个属性，start定义标号的初始值和reversed反项编排属性

### video
		<video controls="controls">
				controls是值播放器的默认样式
				<source src=""> <source src="">
				多个source为了兼容多个浏览器 您的浏览器不支持
		 </video>

> 暂停/播放、放大、缩小自定义js代码

		 var v=document.getElementById();
		 function click1(){
			if (v.paused) v.play();
		 }  else {
			 v.pause();
		 }
		 function clickbig(){
			v.width=800;
			v.height:800;
		}
