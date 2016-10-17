---
title: 初学webpack（二）
date: 2016-10-14 11:02:45
tags: webpack
categories: webpack
---
原文摘自与：[入门webpack,看这篇就够了](http://www.jianshu.com/p/42e11515c10f)

webpack是打包工具，只负责将css，js等打包
gulp 是自动化任务流程工具
webpack + gulp 绝配 因为webpack可以是gulp中的一个任务专门用来执行打包功能，也不会影响其他任务的执行（自己的简单理解，后续再深入了解）

### 首先全局安装webpack

	npm install webpack -g

### 初始化项目
> 录入一些提示的信息然后，创建一个package.json文件

	npm init

### 安装本地webpack

	npm install webpack --save-dev

### 开始创建文件目录结构

创建两个文件夹app和public，app用来存储原始数据和js模块，public用来存放生成后的文件+index.html, public是用于浏览器访问读取数据的，
在app中创建两个文件，greeter.js和main.js

greeter.js

``` bash
	var defaultData = function () {
	    var greet = document.createElement("div");
	    greet.textContent = "greet";
	    return greet;
	};
	
	module.exports = defaultData;
```

main.js

``` bash
	var greet = require('./greeter.js');
	document.getElementById("root").appendChild(greet());
	// 注意这里要加（）加（）是执行，如果不加（） 就是函数
```

index.html

``` bash
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>webpack demo2</title>
	</head>
	<body>
	    <div id="root"></div>
	    <script src="bundle.js"></script>
	</body>
	</html>
```

webpack.config.js

``` bash
	module.exports = {
	    entry: __dirname + "/app/main.js", // 唯一入口文件
	    output: {
	        path: __dirname + "/public", // 打包后文件输出目录
	        filename: "bundle.js" // 打包后，输出的文件名
	    }
	}
```

> 这里的__dirname是node中的一种全局变量，他只的是当前执行脚本的所在目录

### 配置package.json的script
为了更快的执行任务，进行配置，配置之后使用简单的npm start命令即可，代替 webpack

配置如下：

``` bash
	{
	  "name": "webpack-demo2", // package.json的name属性不能跟webpack命令一样
	  "version": "1.0.0",
	  "description": "webpack实例",
	  "main": "index.js",
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1",
	    "start": "webpack"
	  },
	  "author": "sunnyRui",
	  "license": "ISC"
	}

```

> start是npm一个特殊的脚本名称，所以配置完之后可以直接执行，npm start，如果脚本名称不是start则需执行npm run {script name}


### 生成source maps（使调试更容易）
生成的文件都是合并的，所以不利于调试，通过这个配置，生成source map文件，此文件对应生后的文件，代码可读性更高，便于读取

<table style="margin-top:-430px" cellspacing=0>
	<tr>
		<th>devtool选项</th>
		<th>配置项</th>
	</tr>
	<tr>
		<td>source-map</td>
		<td>在一个单独的文件中产生一个完整且功能完全的文件。这个文件具有最好的source map，但是它会减慢打包文件的构建速度；</td>
	</tr>
	<tr>
		<td>cheap-module-source-map</td>
		<td>在一个单独的文件中生成一个不带列映射的map，不带列映射提高项目构建速度，但是也使得浏览器开发者工具只能对应到具体的行，不能对应到具体的列（符号），会对调试造成不便；</td>
	</tr>
	<tr>
		<td>eval-source-map</td>
		<td>使用eval打包源文件模块，在同一个文件中生成干净的完整的source map。这个选项可以在不影响构建速度的前提下生成完整的sourcemap，但是对打包后输出的JS文件的执行具有性能和安全的隐患。不过在开发阶段这是一个非常好的选项，但是在生产阶段一定不要用这个选项；
	</tr>
	<tr>
		<td>cheap-module-eval-source-map</td>
		<td>这是在打包文件时最快的生成source map的方法，生成的Source Map 会和打包后的JavaScript文件同行显示，没有列映射，和eval-source-map选项具有相似的缺点；</td>
	</tr>
</table>

``` bash
	module.exports = {
	    devtools:'eval-source-map',// 配置生成npm-debug.log文件，选择合适的选项，
	    entry: __dirname + "/app/main.js", // 唯一入口文件
	    output: {
	        path: __dirname + "/public", // 打包后文件输出目录
	        filename: "bundle.js" // 打包后，输出的文件名
	    }
	}
```

### 构建本地服务
监听入口文件的变化，自动刷新页面

安装插件

	npm install webpack-dev-server --save-dev

<table style="margin-top:-530px" cellspacing=0>
	<tr>
		<th>dev-server配置选项</th>
		<th>功能描述</th>
	</tr>
	<tr>
		<td>contentBase</td>
		<td>默认为根目录提供本地服务，如果想在另一个目录有本地服务，则设置其所在目录</td>
	</tr>
	<tr>
		<td>port</td>
		<td>设置默认端口，如果省略，默认为8080</td>
	</tr>
	<tr>
		<td>inline</td>
		<td>设置为true，原文件改变后会自动刷新页面</td>
	</tr>
	<tr>
		<td>colors</td>
		<td>使得终端输出文件为彩色</td>
	</tr>
	<tr>
		<td>historyApiFallback</td>
		<td>在开发单页应用时，非常有用，他依赖于html5 HistoryApi，如果设置为true，所有跳转将指向index.html</td>
	</tr>
</table>

配置到webpack.config.js

``` bash
	module.exports = {
	    devtools:'eval-source-map',// 配置生成source-map，选择合适的选项，
	    entry: __dirname + "/app/main.js", // 唯一入口文件
	    output: {
	        path: __dirname + "/public", // 打包后文件输出目录
	        filename: "bundle.js" // 打包后，输出的文件名
	    },
	    devServer: {
	        contentBase:"./public", // 启动public下的文件
	        colors:true,// 终端输出结果为彩色
	        historyApiFallback:true,// 不跳转
	        inline:true// 实时刷新
	    }
	}
```

此时在命令行下执行webpack-dev-server 就会在public下启动服务，浏览localhost：8080即可看到public下面index.html的内容 

为了方便启动，在package.json里配置一下scripts, 执行npm run dev即可

		scripts：{
			“dev”: "webpack-dev-server --hot --inline" // 注意写法
		}

### loaders

通过使用不同的loader，webpack通过调用外部的脚本或工具可以对各种各样的格式的文件进行处理，比如说分析JSON文件并把它转换为JavaScript文件，或者说把下一代的JS文件（ES6，ES7)转换为现代浏览器可以识别的JS文件。或者说对React的开发而言，合适的Loaders可以把React的JSX文件转换为JS文件。

> loaders 需要单独安装并需要在webpack.config.js下的modules关键字下进行配置，loaders配置选项详解：

* test：匹配loaders所处理文件的扩展名的正则表达式（必须）,
* loader: loader的名称（必须）
* include/exclude: 手动添加必须处理的文件（文件夹）或屏蔽不需要处理的文件（文件夹）（可选）
* query：为loaders提供额外的设置选项（可选）

继续上面的例子，我们吧greeter.js里的问候消息放在一个单独的json文件里，并通过合适的配置使greeter.js可以读取json文件里的值，配置如下：

``` bash
	module:{ // 注意这是module而不是modules
        loaders:[
            {
                test:/\.json$/,
                loader: 'json'
            }
        ]
    }
```
config.json
``` bash
	{
	  "greetJson":"loaders 转换json文件"
	}
```
greeter.js

``` bash
	var greetJson = require('./config.json');

	var defaultData = function () {
	    var greet = document.createElement("div");
	    greet.textContent = greetJson.greetJson;
	    return greet;
	};
	
	module.exports = defaultData;
```

安装json-loader:

	npm install json-loader --save-dev

运行 ：

	npm run dev

### Babel

Babel是一个编译JavaScript的平台，他的强大之处是可以编译以下两种情况：
* 未被当前浏览器支持的es6，可以编译成浏览器支持的es5
* 可以编译基于js进行拓展的语言，例如：react的jsx

#### babel的安装与配置
Babel是几个模块化的包，他的核心是npm中的babel-core,你需要的每一个功能或拓展都需要安装单独的包，用的最多的是**解析es6的babel-preset-es2015**和**解析jsx的babel-preset-react**

我们一次性来安装这些依赖包：

	// 一次性安装多个包，包之间用空格
	npm install --save-dev babel-core babel-loader babel-preset-es2015  babel-preset-react

webpack.config.js配置如下：

	module:{ // 注意这是module而不是modules
        loaders:[
            {
                test:/\.json$/,
                loader: "json"
            },
            {
                test:/\.js$/,
                loader:"babel",
		  exclude: '/node_modules/',
                query: {
                    presets: ['es2015','react']
                }
            }
        ]
    }

现在就可以使用es6以及jsx的语法了，我们用react对上面例子进行测试，先安装react和react-dom

	npm install --save-dev react react-dom

greeter.js

``` bash
	import React, {Component} from 'react';
	import greetJson from './config.json';
	
	class Greeter extends Component {
		render() {
			return (
				<div>
				 	{greetJson.greetJson}
				</div>
			)
		}
	}
export default Greeter;
```

main.js

``` bash
	import React from 'react';
	import {render} from 'react-dom';
	import Greet from './greeter';
	render(
		<Greet/>,
		 document.getElementById('root')
	);
```

### 一切皆模块

webpack把所有的文件都可以当做模块处理，只要有合适的loaders，例如js，css，fonts，图片等等

### 打包css
webpack提供两个工具处理样式表，css-loader和style-loader,css-loader使你能够使用import或require（）的功能，style-loader将所有计算后的样式加入页面中，二者组合能够把样式表嵌入webpack打包后的js文件中

继续上面的例子：安装css-loader，style-loader
	npm install --save-dev css-loader style-loader 
	// 注意save-dev的顺序 如果安装多个模块必须放在 install后面

配置如下：
``` bash
 module:{ // 注意这是module而不是modules
        loaders:[
            {
                test:/\.json$/,
                loader: "json"
            },
            {
                test:/\.js$/,
                loader:"babel",
                exclude: '/node_modules/',
                query: {
                    presets: ['es2015','react']
                }
            },
            {
                test:'/\.css$/',
                loader:"style!css" // 添加对样式表的处理
            }
        ]
    },
```

> loader自右向左顺序执行，！表示一个文件可以使用不同类型的loader

在app文件夹里创建一个main.css文件

``` bash
html {
  box-sizing: border-box;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}

*, *:before, *:after {
  box-sizing: inherit;
}

body {
  margin: 0;
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
}

h1, h2, h3, h4, h5, h6, p, ul {
  margin: 0;
  padding: 0;
}
```
webpack是单一入口，只有通过require或import路径才能导入到相应位置，所以为了找到main.css，在main.js中引入main.css

main.js

```bash
import React from 'react';
import {render} from 'react-dom';
import Greet from './greeter';
import './main.css';   // 引入样式

render(
	<Greet/>,
	 document.getElementById('root')
);
```
> 此时css以内联的方式被引进了index.html中，css也可以打包到单独的文件要通过html-webpack-plugin插件

### css预处理器
#### postcss
为css代码自动添加适应不同浏览器的css前缀

首先安装postcss-loader 和 autoprefixer(这个是自动添加前缀的插件)

	npm install --save-dev postcss-loader autoprefixer

现在配置webpack.config.js

> 需要新建一个postcss关键字，并在里面申明依赖的插件，现在写的css会自动根据can I use 里得数据添加不同前缀了

``` bash
	module.exports = {
	    devtools:'eval-source-map',// 配置生成source-map，选择合适的选项，
	    entry: __dirname + "/app/main.js", // 唯一入口文件
	    output: {
	        path: __dirname + "/public", // 打包后文件输出目录
	        filename: "bundle.js" // 打包后，输出的文件名
	    },
	    module:{ // 注意这是module而不是modules
	        loaders:[
	            {
	                test:/\.json$/,
	                loader: "json"
	            },
	            {
	                test:/\.js$/,
	                loader:"babel",
	                exclude: '/node_modules/',
	                query: {
	                    presets: ['es2015','react']
	                }
	            },
	            {
	               test:/\.css$/,
	                loader:"style!css!postcss" //给css3元素自动加前缀
	            }
	        ]
	    },
	    postcss:[ // 注意这是数组，不是对象
	          require("autoprefixer") // 调用自动添加前缀的插件
	    ],
	    devServer: {
	        contentBase:"./public", // 启动public下的文件
	        colors:true,// 终端输出结果为彩色
	        historyApiFallback:true,// 不跳转
	        inline:true// 实时刷新
	    }
	}
```

运行 npm start 查看浏览器源码 head>style即可看到，自动加了前缀

### 插件（plugins）
插件（Plugins）是用来拓展webpack功能的，他们会在整个构建过程中生效，执行相关任务。
* 在这里我们区分一下loaders和plugins
loaders：在打包构建过程中用来处理源文件（jsx，scss, less..)一次处理一个
plugins：是在整个构建过程中起作用

> webpack 有很多内置的插件，同时也有很多第三方的插件，可以让我们完成更加丰富的功能

#### 使用插件
要使用某个插件，首先通过 npm 安装 ，然后在webpack中配置plugins关键字（是一个数组）

例如：添加一个版权声明的插件
``` bash
var webpack = require("webpack");
module.exports = {
    devtools:'eval-source-map',// 配置生成source-map，选择合适的选项，
    entry: __dirname + "/app/main.js", // 唯一入口文件
    output: {
        path: __dirname + "/public", // 打包后文件输出目录
        filename: "bundle.js" // 打包后，输出的文件名
    },
    module:{ // 注意这是module而不是modules
        loaders:[
            {
                test:/\.json$/,
                loader: "json"
            },
            {
                test:/\.js$/,
                loader:"babel",
                exclude: '/node_modules/',
                query: {
                    presets: ['es2015','react']
                }
            },
            {
               test:/\.css$/,
                loader:"style!css!postcss" // 添加对样式表的处理
            }
        ]
    },
    postcss:[
          require("autoprefixer") // 调用自动添加前缀的插件
    ],
    plugins:[
        new webpack.BannerPlugin("copyRight Flying")
    ],
    devServer: {
        contentBase:"./public", // 启动public下的文件
        colors:true,// 终端输出结果为彩色
        historyApiFallback:true,// 不跳转
        inline:true// 实时刷新
    }
}
```

npm start运行之后，生成的bundle.js的最上面会出现copyRight Flying 版权声明

### HtmlWebpackPlugin
这个插件的作用是依据一个简单的模板，帮你生成最终的html5文件，这个文件自动引用了你打包后的js文件。每次编译都在文件名中插入一个不同的哈希值

安装：

	npm insatll --save-dev html-webpack-plugin

操作：
1. 移除public文件夹，利用此插件，html5文件会自动生成，此外css已经通过前面的操作打包到了js中
2. 在app目录下创建一个html文件模板，这个模板包含title等其他你需要的元素，在编译过程中，本插件会依据此模板生成最终的html页面，会自动添加所依赖的css，js，favicon等文件，在本例中我们命名模板文件名称为index.tmpl.html, 模板源代码：

	``` bash
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>webpack demo2</title>
	</head>
	<body>
	    <div id="root"></div>
	</body>
	</html>
	```
3. 更新webpack的配置文件，方法同上，新建一个build文件夹用来存放最终的输出文件

``` bash
var webpack = require("webpack");
//import webpack from "webpack"; 注意配置文件中不能用import，其他文件可以
var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    devtools:'eval-source-map',// 配置生成source-map，选择合适的选项，
    entry: __dirname + "/app/main.js", // 唯一入口文件
    output: {
        path: __dirname + "/build", // 打包后文件输出目录
        filename: "bundle.js" // 打包后，输出的文件名
    },
    module:{ // 注意这是module而不是modules
        loaders:[
            {
                test:/\.json$/,
                loader: "json"
            },
            {
                test:/\.js$/,
                loader:"babel",
                exclude: '/node_modules/',
                query: {
                    presets: ['es2015','react']
                }
            },
            {
               test:/\.css$/,
                loader:"style!css!postcss" // 添加对样式表的处理
            }
        ]
    },
    postcss:[
          require("autoprefixer") // 调用自动添加前缀的插件
    ],
    plugins:[
        new HtmlWebpackPlugin({
            template: __dirname+"/app/index.tmpl.html"
        })
    ],
    devServer: {
        contentBase:"./public", // 启动public下的文件
        colors:true,// 终端输出结果为彩色
        historyApiFallback:true,// 不跳转
        inline:true// 实时刷新
    }
}
```

进行到html-webpack-plugin，可能是网速原因还没有安装成功，，待续。。。。






[github上Demo地址](https://github.com/rui-noworry/myWeb/tree/master/webpack-demo2)