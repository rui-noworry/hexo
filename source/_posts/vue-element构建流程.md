---
title: vue + element构建流程
date: 2017-06-20 18:08:44
tags: vue
category: vue
---

#### 1. 执行安装步骤npm vue的脚手架 vue-cli

#### 2. npm element-ui

### 3. 在入口文件main.js执行
```bash
  import ElementUI from 'element-ui'
  import 'element-ui/lib/theme-default/index.css'
  Vue.use(ElementUI)
```
### 4. .babelrc中

  > 按需引入组件的作用 安装插件 babel-plugin-component
```bash
  "plugins": [
    [
      "component",
      [
        {
          "libraryName": "element-ui",
          "styleLibraryName": "theme-default"
        }
      ]
    ]
  ],
```
### 5. 此时app.vue中测试一下即可使用<el-button>等element-ui的相关组件

### 6. 使用scss 即 style中 lang=scss

### 7. 安装
```bash
    "sass-loader": "^6.0.3",
    "scss-loader": "0.0.1",
    "style-loader": "^0.13.2",
    "node-sass": "^4.5.0",
```
> 不再需要配置，因为webpack已经配置了vue-loader

### 8. eslint也不需要安装，vue-cli脚手架已经给配置好

### 9. 配置文件输出目录public

> config/index中配置将dist改成public


### 10. babel-preset-es2015 转换插件

### 配置：
> router.js 就是配置一些url方便的配置
``` bash
export default new Router({
    mode: 'history', // 显示正常的url
    routes,
    base: ‘./views’// url前缀的意思

})
```
### 入口文件
main.js 配置一些第三方插件等等

### vuex
> 所有的vuex配置都在store/index.js里
  使用vuex只需 在 app.vue里引入store/index.js  import store from './store/index'



初次配置项目： 用webstorm创建一个express服务 然后 创建assets的前端项目

** 构建的时候注意的问题：vue和vue-template-compiler的版本要对应 否则会编译错误
线上环境配置：devtool: config.build.productionSourceMap ? '#source-map' : false, 可以在线上看到sourse-map像在本地看js代码一样方便调试 **

写style注意：
```bash
<style lang='scss' rel="stylesheet/scss">加  rel="stylesheet/scss"是为了写样式的时候有提示
```
