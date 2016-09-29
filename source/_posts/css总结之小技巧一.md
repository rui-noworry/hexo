---
title: css总结之小技巧一
date: 2016-09-27 17:07:13
tags: css
categories: css
---

## 背景渐变，先写颜色值再写百分比

		background:-webkit-linear-gradient(top, #4BA335 10%, #4BA33E 50%, #00ff00 100%)

## 响应式图片自适应

- 单一背景图自适应

		background-size:cover;

- img图片自适应：给div设置百分比的宽度, img的宽高设置：

		width：100%
		height：100%

## 文字阴影用法同box-shadow

		text-shadow：3px 5px 1px #000;

## 文字换行

``` bash
Word-break:normal （浏览器默认换行）
Keep-all（在字符串连接处或者半角处换行）
break-all （可以在单词某个字母处换行）
```

## 修改字体类型，保持字体大小不变

> 0.60是aspact值，这个值是font-size/x-height(字体的高度) 通过微调aspect值使各种字体高度相同

		font-size-adjust:0.60;

## 清除浮动的方法

        .clearfix:after{
            Content:””;
            width:0;
            height:0;
            clear:both;
            overflow:hidden;
            或者
            Content:””;
            display:block;
            clear:both;
            overflow:hidden;
        }

## 文字的高度问题

> 若容器的高度为50px但是当你把鼠标放上的时候会高一点是因为有line-height，当line-height=1的时候字体的高度=容器的高度

## 单行文本溢出

		.online {
			overflow:hidden;
			white-space:nowrap;
			text-overflow:ellipsis;
		}

## 多行文本溢出

> 方向：垂直的
>  -webkit-line-clamp: 2 只显示两行，第二行后面显示…

		.lintwoline{
			Display:-webkit-box !important;
			Overflow:hidden;
			 Text-overflow:ellipsis;
			Word-break:break-all;
			-webkit-box-orient:vertical;
		 }
