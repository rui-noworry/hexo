---
title: window.onload问题总结
date: 2016-10-12 16:07:43
tags: js
categories: js
---

## window.onload问题

最近做了一个wap的组图功能，**要求图片在显示区域居中**（这也是出现问题的地方），因为当时刚刚接触wap移动端还不知道swiper这个东西，所以用hammer.min.js这个插件自己手写了一个图片轮播，本地测试没有问题，发布到线上出现了问题，本地没问题，线上有问题，顿时就蒙圈了，后来请教身边的大牛才知道原因，竟是 图片的加载顺序问题

问题：线上网速较慢，图片过大，加载速度很慢，所以图片顺序执行的时候没有获取到图片的高度，所以导致图片上方有很大的距离，因为我当时用的jquery，$(function(){ }) 也就是$(document).ready()

知识点：$(document).ready()和window.onload的区别

解决：
	``` bash
	$("img")[0].onload = function(){
		// 为了万无一失
		setTimeout(function(){

		}, 0);
	}
	```
**$(document).ready()是等待所有Dom节点加载完成之后执行**
**window.onload是页面里的所有节点包括Dom，图片等所有元素都加载完才执行**

> 其中隐藏了一个知识点是setTimeout, 如果执行完某一个程序之后需要立即执行下一个程序，可以使用：

	setTimeout(function(),0)

