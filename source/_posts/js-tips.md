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

### this指向

> es6箭头函数的this永远指向的是所在对象的最外层，es5的this指向的是调用者
function中的this默认指向的是window

### promise
> Promise 必须有返回值，错误的结果也要接收返回值，否则无法接收结果

*用法，首先引入Promise

```javascript

    import {Promise} from 'es6-promise'
    //同时请求多个方法
    Promise.all([
         Account.getCard(this.user.id),
             Account.bankList()
         ]).then((values)=> {
              this.oldCardInfo = values[0] || {};
              this.banks = values[1];
    });

```
逻辑判断要严谨，例如在使用promise的时候：
1. 成功返回数据 - 数据为空的情况 then
2. 服务器返回error的情况 catch

### mouseover mouseenter mouseout mouseleave区别

> mouseenter:
  事件在鼠标进入某个元素，或第一次进入这个元素的某个子元素时触发。一旦触发后，
  在mouseleave之前，鼠标在这个元素的子元素上触发mouseenter事件都不会触发这个元素的mouseenter事件。
  即：一旦进入，在子元素间的mouseenter不算是在本元素上的mouseenter。

  mouseover:
  事件是必然冒泡的，一旦子元素mouseover了，本元素必然mouseover（除非子元素上禁止冒泡了）
  (在子元素上移动必然一直触发mouseover和mouseout)

### target


### array 相关
1. Math.max.apply(Math, [1,2,3]  获取一组数的最大值

   Math.max(1, 3, 4, 5, 6) 获取最大值

   min 同理

> 获取dom时间的 当前 触发对象 e.currentTarget

### jquery.validate() 相关
1. 对隐藏元素不进行验证
   解决方案：$('#detail').validate({
    ignore: [], // 置空
    rules: {}
   });
2. 如果动态追加验证
   解决方案：$('input[name="color"]').rules('add', {require: true})

### jquery datatables 相关
1. 删除某一行的数据
   var dtcot = $('#table').DataTable({
   		sDom: "Tt<'row-fluid'<'span6'i><'span6'p>>",
   		bSort : false,
   		oTableTools : {aButtons:[]},
   		aoColumns : tableView.columnData
   });
   dtcot.fnDeleteRow($(this).parentsUntil('tr').parent()[0])
2. 如果想动态生成datatable ，就在事件里重新定义，不能重复定义，会报错

3.动态的生成列
    data.forEach(pitem=>{
		let obj = {};
		obj.mData = function(item){
		    return cellRenderer(item, pitem.columnName) // 显示列的字段值
		};
		obj.sTitle = pitem.columnNameCN; // 显示列的标题
		tableView.columnData.push(obj);
    });
4. console.log(dtcot) 可以了解获取所有属性和方法