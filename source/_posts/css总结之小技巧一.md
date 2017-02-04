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


## 标签嵌套问题
> 例如：在浏览器中渲染的时候会展示成两个两个并列的a

		<a href=""><a href="">非法嵌套</a></a>
		<p> <p></p> </p>

*  注意在做详情介绍的时候外层标签不能用p，编辑器上传的数据可能含有p标签*

## 显示固定的函数多余显示...

```bash
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-box-orient: vertical
    -webkit-line-clamp: 3;
```
> 如果设置box会对当前样式产生影响，再给他加一个父层

## display:inline-block代替float:left

> 并排显示的inline-block元素，父层设置了font-size：0 letter-spacing：-3px子元素就会显示在一行，但在uc浏览器中可能也会折行，因为标签间的折行会起作

* 解决去掉标签与标签之间的回车和空格

## 关于textarea实现文本的左对齐

> textarea会把开始标签到结束标签里的内容全部原样显示，包括空格和代码。

例如：你的代码是这样写的：
```bash
<textarea rows="" cols="">   content</textarea>，特别是我们不注意的时候：
<textarea rows="" cols="">content
</textarea>这样进行换行，也被看做是空格，所以也就不能实现对齐了，要想始终保持左对齐必须：
<textarea rows="" cols="">content</textarea>这样没有空格
```

## 去掉input在浏览器中默认的 右侧叉号
``` bash
    input[type="search"]::-webkit-search-cancel-button{
        display:none;
    }
```