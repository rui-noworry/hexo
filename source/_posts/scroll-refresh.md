---
title: scroll-refresh
date: 2016-12-27 17:27:32
tags: js
categories: js
---

## 移动端实现下拉刷新

> 实现思路：通过下拉的动作控制显示层的高度，实现下拉的效果

* html部分

``` bash
    <meta charset="utf-8"/>
    <title>Pull to Refresh</title>
    <meta name="viewport"
        content="width=device-width,height=device-height,inital-scale=1.0,maximum-scale=1.0,user-scalable=no;"/>

    <div class="outerScroller">
        <div class="icon-refresh">
            <span><i class='arrow'></i> 加载</span>
        </div>
        <ul class='scroll'>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>6</li>
            <li>7</li>
            <li>8</li>
            <li>9</li>
            <li>10</li>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>6</li>
            <li>7</li>
            <li>8</li>
            <li>9</li>
            <li>10</li>
        </ul>
    </div>
```

* css部分

``` bash
    <style>
            * {
                padding: 0;
                margin: 0;
            }

            .icon-refresh {
                display: flex;
                align-items: center;
                justify-content: center;
                height: 0;
                overflow: hidden;
            }
            .icon-refresh > span {
                font-size: 12px;
            }
            .arrow {
                display: inline-block;
                width: 16px;
                height: 16px;
                background: url("./images/arrow.png") no-repeat;
                background-size:cover;
                transform: rotate(0deg);
            }
            /*.arrow:hover{*/
                /*transform: rotate(180deg);*/
                /*-webkit-transition: transform .3s ease;*/
            /*}*/
            .arrow-btm {
                transform: rotate(180deg);
                -webkit-transition: transform .3s ease;
            }

            li {
                list-style-type: none;
                height: 35px;
                background: #ccc;
                border-bottom: solid 1px #fff;
                text-align: left;
                line-height: 35px;
                padding-left: 15px;
            }

            .scroll {
                width: 100%;
            }
        </style>
```

* js部分

``` bash
    <script>
        var scroll = document.querySelector('.scroll');
        var outerScroller = document.querySelector('.outerScroller');
        var refresh = document.querySelector('.icon-refresh');
        var touchStart = 0; // 起始点位置
        var reHeight = 0; // 下拉高度

        outerScroller.addEventListener('touchstart', function (event) {
            /* 判断刷新dom是不是在可视窗口，如果不在可视窗口不加载数据
            在数据过多向上滑动的时候会出现问题 */
            var react = refresh.getBoundingClientRect();
            if (react.top < 0) {
                return;
            }

            // 下拉高度重置
            var touch = event.touches[0];

            // 把元素放在手指所在的位置
            touchStart = touch.pageY;

            // 把这两个方法放在这里是为了避免列表数据太多向上滑动的时候，依然会加载数据，所以要在这判断
            this.addEventListener('touchmove', moveProcess, false);
            this.addEventListener('touchend', moveEnd, false);

        }, false);

        // 滑动过程
        function moveProcess(event) {
            // 设置下拉框中显示的内容
            setState(1);

            var touch = event.touches[0];

            // 阻止浏览器默认事件
            if (touch.pageY > touchStart) {
                event.preventDefault();
            }
            // 获取下拉高度
            reHeight = (touch.pageY - touchStart) / 3; // 为了防止下拉高度过大，所以除一定数值

            if (reHeight > 40) {
                setState(2);
            }
            refresh.style.height = reHeight + 'px'
        }
        // 滑动结束
        function moveEnd() {
            // 一定要移除事件，否则会一直监听
            outerScroller.removeEventListener('touchmove', moveProcess);
            if (reHeight > 40) {
                refreshAjax();
                setState(3);
            }

            setTimeout(function () {
                refresh.style.height = 0;
            }, 100)
            outerScroller.removeEventListener('touchend', moveEnd);
        }

        function refreshAjax() {
            for (var i = 1; i > 0; i--) {
                var node = document.createElement("li");
                node.innerHTML = "I'm new";
                scroll.insertBefore(node, scroll.firstChild);
            }
        }

        // 设置下拉框中的内容
        function setState(num) {
            if (num == 1) {
                refresh.querySelector('span').innerHTML = "<i class='arrow'></i> 加载";
            } else if (num == 2) {
                refresh.querySelector('span').querySelector('i').classList.add('arrow-btm');
            } else if (num == 3) {
                refresh.querySelector('span').innerHTML = "加载中";
            }
        }
    </script>
```
