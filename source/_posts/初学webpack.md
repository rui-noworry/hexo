---
title: 初学webpack
date: 2016-10-11 14:34:28
tags: webpack
categories: webpack
---

## webpack
原文 摘自与 慕课网的 [快速入门 webpack](http://www.imooc.com/article/10965)

查找资料，总结成笔记，对于大牛来说webpack简单易懂容易上手，但是对我这个小菜鸟来说，还需一番折腾与实践，已经看了数日，但是似乎没有捋顺其中的逻辑，所以写此文来细细琢磨一番！

### 什么是webpack
> webpack就是一个模块打包工具，处理模块之间的依赖，同时生成对应模块的静态资源

#### 要点：
- webpack 把项目中的所有资源看做是一个模块
- 模块之间存在这一系列的依赖
- 打包之后生成多个静态文件，涉及到代码拆分，提取，合并

### webpack安装与配置
#### 安装
为了加快安装的速度，可以先安装淘宝镜像
npm install -g cnpm --registry=https://registry.npm.taobao.org

- 全局安装（以便全局调用：如webpack --config webpack.config.js）

		npm install -g webpack
- 项目本地安装

		npm install webpack (--save-dev 加不加即可,加上--save-dev会将配置写在package.json里如果不加直接安装在本地，不会写入package.json)
		// 本地安装是为了方便调用
		方式一：es6 语法
		import webpack from "webpack"
		方式二：es5 语法
		var webpack = require("webpack")

### webpack的基本配置

- 创建配置文件（webpack.config.js）,执行webpack命令的时候，默认会执行这个文件

``` bash
	module.export = {
		entry: "app.js", // 入口文件
		output: {
			path: 'assets/', // 输出文件所在的目录
			filename: '[name].bundle.js'	// 输出文件名，name是入口文件定义的名字 输出文件夹是app.bundle.js
			---------不确定
		}，
		module： {
			loaders:[
				// 使用babel-loader解析js或者jsx模块
				{test:/\.js\.jsx%/, loader: 'babel'}，
				// 使用css-loader解析css模块
				{test:/\.css$/, loader:'style!css'}
			]
		}

	}
```
解析css另一种写法是：{test:/\.css$/, loader:['style', 'css']}

### 一个简单的例子
**以下是我实践过的例子，并标注了容易出错的地方**

目录结构是这样的：
- index.html
- basic
	- assets
	- node_modules
	- app.js
	- app.css
	- package.json
	- webpack.config.js


webpack.config.js
``` bash
	module.exports = {
	    // 如果你有多个入口js文件，需要打包在一个文件夹中，这样写：
	    // entry: ['./app1.js', './app2.js']
	    entry:'./app.js',
	    output:{
	        path:'./assets',
	        filename:'[name].bundle.js'
	    },
	    module:{
	        loaders :[ // 注意是loaders 不要少了s
	            {test:/\.js$/, loader:'babel'}, // 注意是test不是text
	            {test:/\.css$/,loader:'style!css'}
	        ]
	    }
	};
```



 如果关键字写错，会报这个错误
![alt text](../uploads/images/error1.png )

app.js

``` bash
	require('./app.css');
	document.getElementById('container').textContent = "App";
```

app.css

``` bash
	* {
	    margin: 0;
	    padding: 0;
	}

	#container {
	    margin: 50px auto;
	    width: 50%;
	    height: 200px;
	    line-height: 200px;
	    border-radius: 5px;
	    box-shadow: 0 0 .5em #000;
	    text-align: center;
	    font-size: 40px;
	    font-weight: bold;
	}
```

index.html

``` bash
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	</head>
	<body>
	    <div id="container"></div>
	    <script src="./basic/assets/main.bundle.js"></script>
	</body>
	</html>
```

>需要注意的问题：
>1. 要安装的模块有 css-loader, style-loader, babel-loader, babel-core
>2. webpack.config.js要和node_modules同级




### loaders相关
### loaders中 ！ 的含义

> 代表加载器的流式调用，例如：

{test：/\.css\.less$/, loader：'style!css!less'}

意思是先使用less加载器来解释less文件，然后使用css加载器来解析less解析后的文件

#### loaders中的include和exclude

> include 表示必须要包含的文件或目录，exclude表示要排除的目录

例如：
我们配置中要排除node_modules目录，写法如下：
``` bash
module：{
	loaders:[
		{
			test:/\.js$/,
			loader: 'babel', // 注意与test可以合并写，也可以分开写
			exclude: nodeModuleDir
		}
	]
}
```

官方建议，最好用include,而且include最好是目录

### resove 相关

#### resove.alias

> 为模块路径设置别名，指定引入路径，减少搜索硬盘的时间, 配置与module同级

例如：
``` bash
	module.exports = {
	   ...
	    resolve : {
		    alias:{
			    jquery : 'app/vender/jquery.min.js'
		    }
	    },
	   ...
	};

```

#### resolve.extensions

> 这个项目的作用是自动加上文件的扩展名

比如你要引入scss文件:

		require('syle.scss')

配置之后，只需这样

		require('style')

``` bash
	module.exports = {
	   ...
	    resolve : {
		    alias:{
			    jquery : 'app/vender/jquery.min.js'
		    },
		   extensions: ["", ".webpack.js", ".js", ".scss"]
	    },
	    ...
	};

```

### externals

> 当我们项目引入一些其他类库的时候，但是又不想类库被构建，就要配置这个参数

``` bash
	moduel.exports = {
		...
		externals : {
			'react' : 'React'
		},
		...
	}
```

externals的key就是require是用的，例如require('react') value表示window.React

### devtool

> 提供了一些方式使代码调试更加方便，因为打包之后代码都是合并的，不利于调试和定位

``` bash
	moduel.exports = {
		...
		devtools : 'eval-source-map',
		...
	}
```

### 抽取多入口文件的公共部分 CommonsChunkPlugin

> 此插件不用安装只需引入webpack模块

我们重新建立一个文件夹叫common, 下面有两个入口文件 app1.js 和app2.js:

``` bash
	// common/app1.js
	console.log('App1');
```
``` bash
	// common/app2.js
	console.log('App2');
```

打包之后生成app1.bundle.js, app2.bundle.js 这个两个文件里会有很多公共部分，我们可以把他们提取出来

所以配置文件中的设置如下：

``` bash
	var webpack = require('webpack')
	module.exports = {
	    // 如果你有多个入口js文件，需要打包在一个文件夹中，这样写：
	    // entry: ['./app1.js', './app2.js']
	    entry:'./app.js',
	    output:{
	        path:'./assets',
	        filename:'[name].bundle.js'
	    },
	    module:{
	        loaders :[ // 注意是loaders 不要少了s
	            {test:/\.js$/, loader:'babel'}, // 注意是test不是text
	            {test:/\.css$/,loader:'style!css'}
	        ]
	    }，
	    plugins:[
			// 实例引入的webpack
			new webpack.optimize.CommonsChunkPlugin('common/common.js')
			// 会在assets下面自动建common文件夹并生成common.js
		]
	};
```
抽取出的公共js为common.js
查看app1.bundle.js就是模块中写的代码，公共部分都提取到common.js中了


### extract-text-webpack-plugin 抽取css文件，打包成css bundle

默认情况下js中require的css文件会在浏览器预览的时候直接引入到index.html在head中生成style属于内联，如果想将css文件提取出来可以按照下面的配置去做：

 app.js
``` bash

	require('./app.css');
	document.getElementById('container').textContent = "App";

```
 app2.js
``` bash
	require('./app2.css');
	document.getElementById('container').textContent = "App2";

```
app.css
``` bash

	* {
	    margin: 0;
	    padding: 0;
	}

	#container {
	    margin: 50px auto;
	    width: 50%;
	    height: 200px;
	    line-height: 200px;
	    border-radius: 5px;
	    box-shadow: 0 0 .5em #000;
	    text-align: center;
	    font-size: 40px;
	    font-weight: bold;
	}

```
app2.css
``` bash

	#container{
	    background: #ff0000;
	}
```

webpack.config.js

``` bash
	var webpack = require('webpack');
	// 安装这个插件 npm install
	var ExtractTextPlugin = require('extract-text-webpack-plugin');
	module.exports = {
	    entry: {
	        app: './app.js',
	        app2: './app2.js'
	    },
	    output:{
	        path:'./assets',
	        filename:'[name].bundle.js'
	    },
	    module:{
	        loaders :[
	            {test:/\.js$/, loader:'babel'},
	            {test:/\.css$/,loader:ExtractTextPlugin.extract("style-loader", "css-loader")}
	        ]
	    },
	    plugins:[
	        new webpack.optimize.CommonsChunkPlugin('common/common.js'),
	        new ExtractTextPlugin("[name].css") // name对应的是入口的key
	    ]
	};
```

最终在assets下面生成app.css和app2.css 可以引入到index.html中

> 如果不使用这个插件就会自动引入，编译成内敛样式，如果使用这个插件就需要**手动引入生成的文件啦**

### extract-text-webpack-plugin

> 这个插件还可以将入口引入的所有css都打包成一个文件

例如：

``` bash
	var webpack = require('webpack');
	// 安装这个插件 npm install
	var ExtractTextPlugin = require('extract-text-webpack-plugin');
	module.exports = {
	    entry: {
	        app: './app.js',
	        app2: './app2.js'
	    },
	    output:{
	        path:'./assets',
	        filename:'[name].bundle.js'
	    },
	    module:{
	        loaders :[
	            {test:/\.js$/, loader:'babel'},
	            {test:/\.css$/,loader:ExtractTextPlugin.extract("style-loader", "css-loader")}
	        ]
	    },
	    plugins:[
	        new webpack.optimize.CommonsChunkPlugin('common/common.js'),
	        new ExtractTextPlugin("style.css",{
	            allChunks: true
	        }) // name对应的是入口的key
	    ]
	};
```

如果有多个入口文件，会将最后一个入口文件里的所有css打包，app.js里的文件被忽略

### 给文件添加版本号 HtmlWebpackPlugin插件

**线上发布**时，防止浏览器缓存静态文件，所以给文件加版本号，有两

例如：
``` bash

var webpack = require('webpack');
var ExtractTextPlugin = require('extract-text-webpack-plugin');
+ var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: {
        app: './app.js',
        app2: './app2.js'
    },
    // entry: './app.js',
    output:{
        path:'./assets',
        +filename:'[name].[hash].bundle.js',
        +publicPath:'http://rui-noworry.github.com/assets'
    },
    module:{
        loaders :[
            {test:/\.js$/, loader:'babel'},
            // {test:/\.css$/, loader:"style!css"}
            {test:/\.css$/,loader:ExtractTextPlugin.extract("style-loader", "css-loader")}
        ]
    },
    plugins:[
        new webpack.optimize.CommonsChunkPlugin('common.js'),
        new ExtractTextPlugin("style.css",{
            allChunks:true
        }),
       + new HtmlWebpackPlugin({
            filename:'./index-release.html',
            template: './index.html',
            inject: 'body'
        })
    ]
};
```

``` bash
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>Title</title>
	    <link type="text/css" rel="stylesheet" href="./assets/style.css" />
	</head>
	<body>
	    <div id="container"></div>
	    <script src="./assets/common.js"></script>
	    <script src="./assets/app.26be6a63cd011a056420.bundle.js"></script>
	</body>
	</html>
```
**注意，index.html一定要和node-module同级，否则会报babel错误**
这个插件加上版本号之后还会 自动加入到发布之后的html中，如果不用这个插件会生成hash文件但是不会自动加进发布之后的html文件

### 关于loader

loader是支持链式执行的，并且由右向左执行，可以由sass-loader,css-loader,style-loader组成

### 布置一个本地服务器

``` bash
	cnpm install -g webpack-dev-server

	// 设置文件移动目录
	webpack-dev-server --content-base basic/

```
如果在node_module所在目录可以直接执行webpack-dev-server
如果不在此目录，则需要指定目录，就执行webpack-dev-server --content-base basic/

### webpack.config.js支持es6语法

依赖的插件：babel-loader，babel-core, babel-preset-es2015

``` bash
	module:{
        loaders :[
            {
                test:/\.js$/,
                loader:'babel',
                query:{
                    presets:['es2015']
                }
            },
            // {test:/\.css$/, loader:"style!css"}
            {test:/\.css$/,loader:ExtractTextPlugin.extract("style-loader", "css-loader")}
        ]
    }
```

注意：test 正则语法





