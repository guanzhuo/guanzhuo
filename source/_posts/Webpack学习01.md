---
title: Webpack学习01
date: 2019-03-08 11:56:35
tags: Webpack
categories:
- Webpack
---

##### Webpack学习01

作者：Tobias Koppers (GitHub：@sokra)

Webpack 3.10+

<div align=center>
    <img width=600 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/code/webView/webpack%E6%A6%82%E8%BF%B0.png'/>
</div>

了解前端工程搭建配置

了解前端优化手段

熟悉通过工具提高开发效率

掌握Webpack常见配置

<div align=center>
    <img width=500 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/code/webView/webpack%E5%AD%A6%E4%B9%A0%E5%9B%BE.png'/>
</div>

模块化开法 

##### JS模块化 

commonJS:一个模块为一个文件，通过module.exports暴露接口，通过require引入模块，同步执行方式

AMD模块化、CMD模块化、UMD模块化、ESM模块化

webpack支持：

- AMD (RequireJS)
- ES Modules(推荐)
- CommonJS  



##### CSS模块化



##### 1、打包器webpack

核心概念：

**Entry**：代码的入口、打包入口，单个或者多个（多页面）

```
//一个入口
module.exports = {
    entry: 'index.js'
}
//多个第一种数组
module.exports = {
    entry: ['index.js','vendor.js']
}
//多个第二种对象（推荐）
module.exports = {
    entry: {
    	index: 'index.js',
        index2: 'index2.js',
    }
}
```

**Output**：打包输出

打包生成文件（bundle）

一个活着多个

```
//一个
module.exports = {
    entry: 'index.js',
    output:{
        filename: 'index.min.js'
    }
}
//多个第二种对象
module.exports = {
    entry: {
    	index: 'index.js',
        index2: 'index2.js',
    },
    output:{
        filename: '[name].min.[hash:5].js'
    }
}
```

**Loaders** ：处理JS之外的东西

处理文件，转化为模块

```
module.exports = {
    module:{
        rules:[
            {
                test: /\.css$/,
                use: 'css-loader'
            }
        ]
    }
}
```

常用loader：

**Plugins** ：代码压缩，混淆代码...

参与整个打包过程，打包优化和压缩，配置编译时的变量

```
const webpack = require('webpack');
module.exports={
    plugins:[
        new webpack.optimize.UglifyJsPlugin() //使用该插件混淆代码
    ]
}
```

Chunk：代码块

Bundle：已经打包的

module：模块



##### Webpack基本使用

###### 命令

webpack -h 参数选项

webpack -v 版本

webpack <entry> [<entry>] <output>

配置

webpack

webpack --config webpack.conf.dev.js 

###### 第三方脚手架

Vue-cli

Angular-cli

React-starter

Webpack-Cli：交互式的初始化项目，迁移项目

