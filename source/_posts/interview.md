---
title: 面试总结
date: 2017-08-24 18:08:26
tags: js
---

#### 1. html5新特性？
> (1) 声明文档类型 <!DOCTYPE html>
  (2) 脚本和链接无需type属性
      例如：<link rel="stylesheet" href="path/to/stylesheet.css" />
           <script src="path/to/script.js">
  (3) 语义化标签：header footer article section hgroup small audio video等
      占位符：placeholder
      文本框的属性：required autofocus pattern正则验证

#### 2. css3新特性？
> https://www.ibm.com/developerworks/cn/web/1202_zhouxiang_css3/

#### 3. cookie和localStorage的区别?
> cookie 最大存储4kb 和服务器通信自带http头 ，如何存储过多的信息，会产生性能问题
         一般由服务器生成 设置失效时间 浏览器生成的，关闭后就失效

> sessionStorage 最大存储5M 浏览器关闭失效  浏览器刷新依然存在 只能保存浏览器，不与服务器通信

> localStorage 最大存储5M 信息一致存在，除非删除 只能保存浏览器，不与服务器通信

#### 4. 闭包的含义？应用场景？
> https://www.zhihu.com/question/19554716
  一般来讲 函数内部可以访问函数外部，但是外部不可以访问内部变量，用了闭包之后，外部可以访问大函数内部的变量
`
    例如：
    function superFn(){
            // 局部变量
            var _super_a = 1;

            var subFn = function(){
              // _super_a++;
              alert('_super_a: ' + _super_a);
            }

            return subFn;
          }

          // superFn() 得到的是subFn，superFn()()等于subFn()
          superFn()();
`


#### 5. 如何定义类和实现继承 （es5 & es6）

#### 6. 如何改变this的指向手写实现？
> 通过call, bind, apply 都可以改变this的指向
`
    var obj = {
        name: 'obj',
        test () {
            console.log(this.name)
        },
    }
    var obj1 = {
        name: 'obj1',
        test (a, b) {
            console.log(a, b, this.name)
        },
    }
    obj1.test.call(obj, 1, 2)
    obj1.test.bind(obj)(1, 2)
    obj1.test.apply(obj, [1, 2])
`

#### 7. 如何实现一个首屏弹层，使一天内如果出现就不再出现，15分钟内没有显示再次弹出

#### 8. cookie有哪些参数
`
    document.coolie = newcookie;(newcookie 是键值对的形式key=value; 以分好分隔)
`
> 参数：path;max-age;domain;expire;secure;

#### 9. 如果禁用了cookie，如何实现登录鉴权

#### 10. 有一个数组[4, 1, 6, 2, 3, 7, 9],如何实现生成一个新数组是偶数显示在坐便奇数显示在后边（不考虑排序）
`
    let arr = [4, 1, 6, 2, 3, 7, 9];
                arr.forEach((item, index) => {
                    if (item % 2 === 0) {
                        let newItem = item;
                        arr.splice(index, 1);
                        arr.unshift(newItem);
                    }
                })
`
#### 11. 如何判断白屏时间

#### 12. 性能优化做过哪些
> express的静态文件的缓存：
`
    express 里 api.js里设置：
    var app = express();
    app.use(express.static('./assets', {
        maxAge: 864000  // one day
    }));
`
> webpack dll打包工具 加快编译速度
  将第三方库和自己写的代码分别打包 提高编译速度
  dll打包后会将第三方库写入mainifest里 只有第三方库没有更新 修改 升级就不需要重新打包编译
  **参考: https://segmentfault.com/a/1190000005969643**

#### 13. 跨域的实现方案
** jsonp **

> 缺点：只能进行get请求， js容易被注入不安全，发生错误后没有错误提示

  优点：支持老式浏览器

** CORS **

>  分为简单请求和非简单请求
   简单请求：请求方法只有post get head
   非简单请求：会发送两次请求，进行“预检”验证，访问服务器是否在访问的范围内，如何可以再进行 xmlhttprequest 正常请求
             包括所有的请求方法
   详情：http://www.ruanyifeng.com/blog/2016/04/cors.html

** postmessage **

> 页面 iframe 多窗口之间的信息传递

#### 14. 了解http协议

#### 15. git pull 和 git fetch 的区别
      git pull  = git fetch + git merge
`
    git fetch origin master:tmp
    git diff tmp
    git merge tmp
`
  从远程获取最新的版本到本地的test分支上之后再进行比较合并
  git pull：相当于是从远程获取最新版本并merge到本地
  git pull origin master

  上述命令其实相当于git fetch 和 git merge
  在实际使用中，git fetch更安全一些
  因为在merge前，我们可以查看更新情况，然后再决定是否合并结束

#### 16. 前端线上和ci部署流程

#### 17. div宽高不确定实现垂直居中
     父层：display: flex; align-items: center; justify-content: center;

#### 18. 如何判断是否为数组数据结构？instanceof 缺点?

#### 19. svg和icon-font的区别（引申svg和canvas的各自优缺点）

#### 20. 理解setTimeout（fn, 0）的含义

#### 21. css单位有哪些，vh和vw的含义？rem和em的区别

#### 22. js时间冒泡和时间捕获的区别，target的含义？ target和srcElement的区别？

#### 23. 用过的es6的方法有哪些

#### 24. 为什么用箭头函数 优缺点

#### 25. call和apply,bind的区别和作用
> http://www.imooc.com/article/17056

#### 26. 输入url敲回车整个过程发生了什么，浏览器渲染html的过程
>  1. 输入url回车之后 浏览器查找浏览器dns缓存 查找系统缓存 查找host
   2. 如果有直接渲染 如果没有进行最近的DNS域名解析 返回 ip
   3. 发起tcp请求 进行三次握手
   4. 握手成功 向服务器发起 http 请求 发送数据包
   5. 服务器接收数据包 并返回
   6. 浏览器接收响应 解析html 生成dom树 解析js 解析css 渲染页面

#### 27. sass ~ 和 + 的区别

#### 28. 写出一个ajax基本配置的代码

#### 29. 123456如何输入123,456或者1,23456

#### 30. 3.567转成两位小数的方法

#### 31. jquery .map() .filter() .every 的区别

#### 32. 伪元素有哪些？ :: 的含义

> 伪类:用于当已有元素处于的某个状态时，为其添加对应的样式
  例如：:active, :hover, :focus, :visited, :link

> 伪元素：:before, :after

> 总结：伪元素和伪类之所以这么容易混淆，是因为他们的效果类似而且写法相仿，但实际上 css3 为了区分两者，已经明确规定了伪类用一个冒号来表示，而伪元素则用两个冒号来表示。

> ::的含义是为了区分伪类和为元素，但是:: 只是对于css3 老浏览器不兼容

### 面试题汇总：

> https://github.com/markyun/My-blog/blob/master/Front-end-Developer-Questions/Questions-and-Answers/README.md