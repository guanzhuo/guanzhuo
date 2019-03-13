---
title: Webpack学习02
date: 2019-03-09 10:32:08
tags: Webpack
categories:
- Webpack
---

#### Webpack学习02

#### 1、编译ES 6/7

Babel

babel-loader



Babel-presets 规范

target参数：制定目标进行编译，指定浏览器和node版本

针对不同浏览器，不同版本进行制定编译

配置文件

```js
module: {
    rules: [
      {
        test: /\.js$/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
              ['@babel/preset-env', {
                targets: {
                  // browsers: ['>1%', 'last 2 versions ']//大于全球1%的浏览器主流浏览器的最新两个版本，数据来源于browserslist和Can I use
                  chrome: 52 //浏览器版本52谷歌
                }
              }]
            ]
          }
        },
        exclude: '/node_modules'
      }
    ]
  }
```

编译前

<div align=center>
    <img width=400 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/code/webView/presets1.png'/>
</div>

编译后

第一个结果：let 、const转为var

<div align=center>
    <img width=400 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/code/webView/presets3.png'/>
</div>

第二次的结果：chrome支持语法，所以编译后基本没变化

<div align=center>
    <img width=400 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/code/webView/presets2.png'/>
</div>



#### 插件：

解析：使用cs6部分函数和方法，如：Generator 、Set、 Map、 Array.form...，需要使用一下插件 

###### 1、Babel Polyfill 全局垫片，为应用准备 

npm install babel-polyfill --save

使用方法：

在入口文件的js加上

```
import 'babel-polyfill'
```

Babel Runtime Transform 局部垫片，不会污染全局，为开发框架准备

就可以使用了



###### 2、Babel Runtime Transform 局部垫片，为框架准备 ，不会污染全局

```
npm install @babel/plugin-transform-runtime --save
npm install @babel/runtime --save
```

新建.babelrc文件，进行配置，将rules中presets放到这里

```
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          "browsers": [
            "last 2 versions"
          ]
        }
      }
    ]
  ],
  "plugins": [
    "@babel/transform-runtime"
  ]
}
```

#### 二、配置Typescript

js的超集

网址：http://www.typescriptlang.org/index.html

typescript-loader

安装：

```
npm i typescript ts-loader --save-dev
npm i typescript awesome-typescript-loader --save-dev
```

配置：

tsconfig.json  官网：http://www.typescriptla ng.org/docs/home.html

webpack.config.js

常用选项：

- compilerOptions
- include
- exclude



a、类型判断，声明文件

安装声明文件：

```
npm install @types/lodash --save
```

文件有错误时会提示

传参错误时，会有编译反馈

b、Typings

安装：

```
npm i typings -g
typings install lodash --save
```

之后会生成一个typings.json文件和typings文件夹

在tsconfig.json文件中增加，指定声明文件的地址：

<div align=center>
    <img width=400 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/code/webView/typings.png'/>
</div>

#### 三、提取公用代码

减少代码冗余

提高加载速度 

使用插件：CommonsChunkPlugin

配置：

#### 四、代码分割和懒加载

