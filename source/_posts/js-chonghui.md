---
title: JS重绘问题
date: 2016-10-08 10:04:55
tags: js
categories: js
---

> 当js功能发生变化，但是页面没有响应，考虑 重绘问题，解决技巧

**操作技巧**

``` bash

	if($('.pic-content').css("visibility") === "inherit")

		$('.pic-content').css("visibility","visible");

	else{

		$('.pic-cntent').css("visibility","inherit");

	}
```

*或用其他样式来触发动作*

**重排重绘 提高性能参考** [相关链接](http://www.cnblogs.com/zichi/p/4720000.html)

