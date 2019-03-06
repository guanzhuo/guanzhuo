---
title: webpack和vue实现Todo应用
date: 2019-03-01 12:04:24
tags: Vue
categories:
- vue项目开发Todo应用
---

##### vue项目开发Todo应用

学习

1、配置搭建前端工程

2、vue实现Todo应用

3、优化webpack打包



npm init 初始化

安装插件：npm i webpack vue vue-loader

安装npm i css-loader url-loader file-loader

vue-loader was used without the corresponding plugin. Make sure to include VueLoaderPlugin in your webpack config.

错误：You may need an appropriate loader to handle this file type

<div align=center>
    <img width=400 src='/images/vueTodo/error1.png'/>
</div>

我在使用require("./style.css");的时候,也就是想要把css文件也一并打包,但是webpack本身是不支持的,所以我们需要安装

```
npm install css-loader style-loader --save-dev
```

安装完成后：

在webpage.config.js中增加style的配置

<div align=center>
    <img width=400 src='/images/vueTodo/r1.png'/>
</div>

```js
module: {
        rules: [
            {
                test: /.vue$/,
                loader: 'vue-loader'
            },{
                test:/\.css$/,
                use:[
                    'style-loader',
                    'css-loader'
                ]
            }
        ]
    }
```

然后就可以使用npm run build进行打包

1、npm更换源

2、npm安装指定版本、卸载、升级

3、dev build、生产开发模式

4、webpack-dev-server

<div align=center>
    <img width=400 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/code/APP%E4%BF%AE%E6%94%B9.png'/>
</div>

npm i rimraf -D     build删除就目录，重新生成dist  

npm i vue-style-loader -D  修改css进行热重载

npm i webpack-merge -D

devdependencies 和 dependencies区别