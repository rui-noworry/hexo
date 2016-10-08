---
title: seajs简单应用
date: 2016-10-08 10:16:42
tags: js
categories: js
---

> 要点：同步加载 依赖就近 延迟执行 什么时候需要什么时候require进来

**例子：index.html**

``` bash
	index.html
	<script type="text/javascript" src="js/sea.js">< /script>

	seajs.config({
	base:"./js/",
	alias:{
	jquery:'jquery-2.2.3.min'
	}
	});

	seajs.use('main');
```

**main.js**
> 所有模块都通过 define 来定义

``` bash
	define(function(require, exports, module) {
	 //  通过 require 引入依赖
	  require('jquery');
	  require.async('index', function(index) {
	   console.log(index.doSomething1());
	  });
	});
```

**index.js 首页模块**

``` bash
	define(function(require, exports, module) {
	  // 通过 exports 对外提供接口
	  var a = {};
	  a.doSomething = function(){
	   console.log("Ok");
	  }
	  a.doSomething1 = function(){
	   console.log("doSomething1");
	  }
	  // 或者通过 module.exports 提供整个接口
	  module.exports = a;
	});
```
