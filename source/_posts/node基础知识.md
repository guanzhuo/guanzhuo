---
title: node基础知识
date: 2019-03-06 15:34:05
tags: 前端技术
categories:
- node基础知识
---

#### Node基础知识

​        Node.js是一个基于Chrome JavaScript运行时建立的平台， 用于方便地搭建响应速度快、易于扩展的网络应用。Node.js 使用事件驱动， 非阻塞I/O模型而得以轻量和高效，非常适合在分布式设备上运行数据密集型的实时应用。Node.js很适合搭建轻量的服务器（应用），所以它又被人称为服务器语言，前端中的后端语言。node翻译过来是节点的意思，而node.js后面特地带了.js，就表示它与JavaScript有莫大的关系。node.js是javascript的一种运行环境，是服务器端的javascript的解释器。

​        npm则是包含在node.js里面的一个包管理工具，就如同linux中的yum仓库，rpm包管理；如同python中的pip包管理工具一样。

##### 一、npm更换源

使用阿里定制的 cnpm 命令行工具代替默认的 npm

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

检测安装信息

```
cnpm -v
```

之后使用cnpm安装即可

##### 二、npm 安装的几种方式

###### 1、安装模块到项目目录下：

```
npm install moduleName # 安装模块到项目目录下
```

安装模块到项目node_modules目录下，这种方式不会将模块依赖写入devDependencies或dependencies 节点，在运行npm install初始化项目时不会下载模块。

###### 2、将模块安装到全局，具体安装到磁盘哪个位置，要看 npm config prefix 的位置：

```
npm install -g moduleName # -g 
```

安装模块到全局，不会在项目node_modules目录中保存模块包。不会将模块依赖写入devDependencies或dependencies 节点。运行 npm install 初始化项目时不会下载模块。

###### 3、将模块安装到项目目录下，并在package.json文件的dependencies节点写入依赖。

```
npm install moduleName -save  # -save 
```

安装模块到项目node_modules目录下。 会将模块依赖写入dependencies 节点。 运行 npm install 初始化项目时，会将模块下载到项目目录下。运行npm install --production或者注明NODE_ENV变量值为production时，**会**自动下载模块到node_modules目录中。

###### 4、将模块安装到项目目录下，并在package.json文件的devDependencies节点写入依赖。

```
npm install moduleName -save-dev  # -save-dev
```

安装模块到项目node_modules目录下。会将模块依赖写入devDependencies 节点。运行 npm install 初始化项目时，会将模块下载到项目目录下。运行npm install --production或者注明NODE_ENV变量值为production时，不会自动下载模块到node_modules目录中。



**devDependencies** 节点下的模块是我们在开发时需要用的，比如项目中使用的 gulp ，压缩css、js的模块。这些模块在我们的项目部署后是不需要的，所以我们可以使用 -save-dev 的形式安装。像 express 这些模块是项目运行必备的，应该安装在 **dependencies** 节点下，所以我们应该使用 -save 的形式安装。

##### 三、npm安装指定版本

```
npm install webpack@3.0.0 -g
```

查询npm安装某个模块的版本

```
npm list [name]
```

查询所有已安装模块的版本

```
npm info styled-components
```

如下图

<div align=center>
    <img width=400 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/code/node/listV.png'/>
</div>

##### 四、更新npm中某个模块

删除版本号 "^2.1.0" ==> ""

在控制台输入：

```
npm install vue -save
```

即可自动安装更新

<div align=center>
    <img width=400 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/code/node/update.png'/>
</div>

npm更新某个模块

```
npm i styled-components@latest \\更新到最新版
npm i styled-components@2.2.1 \\更新到具体某个版本
```

##### 五、卸载模块

删除模块或者删除全局模块

```
# 删除xxx模块；
$ npm uninstall xxx 
# 删除全局模块xxx；
npm uninstall -g xxx
```

