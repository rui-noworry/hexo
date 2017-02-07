---
title: 实现一个简单的小日历功能
date: 2017-02-07 18:06:05
tags: js
---

## 实现一个简单的小日历功能
> 样式待完善

### css
``` bash
    .calender {
        margin-top: 20px;
    }
    .calender span {
        display: inline-block;
        border: 0.5px solid #ddd;
        width: 50px;
        height: 30px;
        line-height: 30px;
        text-align: center;
        vertical-align: top;
        font-size: 14px;
        letter-spacing: 0;
    }
    .calender, .trends{
        letter-spacing: -3px;
        font-size: 0;
    }
```

### html
``` bash
    <!--日历布局-->
        <div><span onclick="arrowLeft()"><<</span><span class="calenderShow">2017年2月</span><span onclick="arrowRight()">>></span></div>
        <div class="calender">
            <div>
                <span>周日</span><span>周一</span><span>周二</span><span>周三</span><span>周四</span><span>周五</span><span>周六</span>
                <div class="trends"></div>
            </div>
        </div>
```

### js
``` bash
    // 获取当前年月
        var month = new Date().getMonth() + 1
        var year = new Date().getFullYear()

        function arrowLeft() {
            month --
            if (month == 0) {
                month = 12
                year --
            }
            getCalender (year, month)
        }

        function arrowRight() {
            month ++
            if (month == 13) {
                month = 1
                year ++
            }
            getCalender (year, month)
        }

        // 获取当月日历
        getCalender (year, month) // 月份从1开始

        // 日历布局
        function getCalender(year, mounth) {
            // 存储日历数据的数组
            var calenderArr = []
            var html = ""
            // 获取本月的第一天是星期几 周日 0 周一 1...
            var firstDay = new Date(year, mounth - 1, 1).getDay() // 参数的月份是从0开始
            // 获取本月一共多少天
            var curMonthdays = new Date(year, mounth, 0).getDate() // 参数的月份从1开始
            var n = 0
            // 行
            for (var i = 0; i < 6; i++) {
                html += "<div>"
                // 列
                for (j = 0; j < 7; j++) {

                    if (j === firstDay || n > 0) {
                        n ++
                    }

                    if (!n && j < firstDay) {
                        calenderArr.push("")
                        html += "<span> </span>"
                    } else if (n && n <= curMonthdays) {
                        calenderArr.push(n)
                        html += "<span>" + n + "</span>"
                    } else if (n && n >= curMonthdays) {
                        calenderArr.push("")
                        html += "<span> </span>"
                    }
                }
                html += "</div>"
                if (n >= curMonthdays) {
                    break
                }
            }
            // 获取容器
            var calenderWrap = document.querySelector('.trends')
            calenderWrap.innerHTML = ""
            calenderWrap.innerHTML += html
            document.querySelector('.calenderShow').innerText = year + "年" + month + "月"
        }
```

> 扩展 获取当前月的天数
``` bash
        function getCurMonthDays () {
            var date = new Date()
            var year = date.getFullYear()
            var mouth = date.getMonth() + 1
            var days = new Date(year, mouth, 0)
            return days.getDate()
        }
```


> 扩展 获取近12个月
``` bash
        function getLast12Months(){
                var last12Months = [];
                var today = new Date();

                var month = today.getMonth() + 1;
                var year = today.getFullYear()
                for(var i = 0; i < 12; i ++){
                    last12Months.push(year + '年' + month + '月')
                    if (month === 1) {
                        year --
                        month = 13
                    }
                    month --
                }
            }
```