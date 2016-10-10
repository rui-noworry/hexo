---
title: js小知识点总结
date: 2016-10-10 16:39:57
tags: js
categories: js
---

### 原生JS操作transform属性

例：
``` bash
 $('.pic-content')[0].style.webkitTransform = "translateX(200px)"
```

### JS遍历Dom节点

例：

``` bash
while(dom.firstChild){
	dom.removeChild(dom.firstChild)
}
```

### Json 相关

> JSON里不能有单引号，全部用双引号

[检测地址](http://www.bejson.com)
