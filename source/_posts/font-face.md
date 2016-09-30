---
title: font-face的用法
date: 2016-09-30 14:58:42
tags: css
categories: css
---

### font + html 实体
> 这些字体都是在这个网址：[网址链接](https://icomoon.io/) 生成好的

		@font-face｛
			font-family:"imooc-ico";
			/*字体格式是固定的；为了考虑浏览器兼容的问题所以四种字体格式都要引用 */
			src:url("../fonts/icomoon.eot"),
			/*ie9的兼容模式*/
			src:url("../fonts/icomoon.eot?iefix") format("embedded-opentype"),
			 /* 其中？iefix是ie6-8 的兼容模式，主要起作用的是？*/
			url("../fonts/icomoon.woff") format("woff"),
			url("../fonts/icomoon.ttf") format("truetype"),
			url("../fonts/icomoon.svg") format("svg"),
			font-weight:normal;
			font-style:normal;
		｝

> 在html中调用的方式
> (其中&#x是固定写法，写在最前面为了在html中解析)

		<li class="music-icon"> & # x fo48 </li>

### font + css

> 给所有小图标加公共样式

		 .icon{
			 font-family:"imooc-icon";
			font-style:normal;
			font-weight:normal;
			 font-size:64px;
			 /*为了更好的显示字体，加上抗锯齿光滑性的样式：*/
			 -webkit-font-smoothing:antialiased;
			 -moz-osx-font-smoothing:grayscale;
		 }

 > font+css加小图标：


		 .music-icon:before{
			 content:"\fo48";
			/*注意要加反斜线转义*/
		 }
