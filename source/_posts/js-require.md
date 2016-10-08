---
title: RequireJs简单应用
date: 2016-10-08 10:39:14
tags: JS
categories: js
---

> 解决：团队合作过程中，出现命名重复的情况等
   要点：异步加载，依赖前置（提前执行完）

** 例子：index.html **

``` bash
	<script type="text/javascript" data-main="js/main" src="js/require.js"></script>
	main.js 入口文件
	requirejs.config({
	baseUrl:'js/',// 要引入库的位置
	paths:{
	jquery:'jquery-2.2.3.min'   // 如果名字过长或路径发生变化可以重新定义名字，也可以不重新定义
	}
	});

	requirejs(['jquery', 'valedate'], function($, valedate){
	console.log(valedate.equal(1,2));
	});
```

** valedate.js 验证模块 **

``` bash
	define(['require'], function($){
	return {
		check:function(){},
		equal:function(str1,str2){
			return str1 ===str2;
		}
	}
	});
```

