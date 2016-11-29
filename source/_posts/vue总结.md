---
title: vue总结
date: 2016-11-24 10:40:07
tags: vue
categories: vue
---

## vue使用心得

> v-on:touchmove.prevent="detailScroll"目的是阻止浏览器的默认事件，detailScroll是自定义的，可以没有内容，但是必须定义

```bash
    <div v-on:touchmove.prevent="detailScroll" v-el:artument-detail class="argument-detail">
```

* 调用
```bash
    method:{
    	detailScroll(){}
    }
```

v-el:artument-detail这个就类似与你给元素加个id，方便js中找到 (html代码中不能使用驼峰（要么都是小写要么是中间线），js使用驼峰，否则不起作用)

获取此元素的调用方法：this.$els.argumentDetail

*（注意如果argumentDetail是个变量，获取方式this.$els[argumentDetail]）

### v-link

vue1.0
用法：v-link="{name: 'course-public-childcat', query:{cid:item.id, name:item.name}, params:{type:item.type,id: item.id}}"

vue2.0
用法:
<router-link :to="{name: 'course-public-childcat', query:{cid:item.id, name:item.name}, params:{type:item.type,id: item.id}}"></router-link>

> params是必传参数，query是可选参数

### 组件之间的通信
```bash
<v_list-lesson :multidelete="multidelete" :listdata="listData" :routetype="routeType" :nodata="isNodata"></v_list-lesson>
```
父组件可以通过 ：冒号自定义的方式像子组件传递属性和方法 子组件通过props接收

如果传递的是方法：

例如：
``` javascript

    父组件：
    	methods: {
                // 删除课程
                multidelete(selectIds) {
                    let tempdata = this.listData.filter(item=> {
                        return selectIds.indexOf(item.contentid) < 0;
                    });

                    this.listData = tempdata;
                    store.actions.setCourselistSelectedIds({selectedIds: []})
                },
    子组件：props: ["listdata", "routetype", 'nodata', 'multidelete'], 接收

    	//删除课程
         deleteLessons(){
              this.multidelete && this.multidelete(this.selectedIds); // 这里会将值返回给父组件
         }
```
> 子组件将要删除的id传递给父组件，父组件执行删除的行为

### 关于绑定样式:class
```bash
<article class="list-lessons-container" :class="{'noborder':nodata,'borderTransparent': routetype == 3}">一个标签里只能写一个:class
```

### 关于computed

> 即使属你放在computed里，dom里的元素或input值是不会响应式的变化

