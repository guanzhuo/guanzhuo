---
title: Hexo+GitHub+阿里云 搭建博客
date: 2019-01-15 15:07:47
tags: Hexo
categories: Hexo
---

## Hexo Blog+阿里云配置

上一篇介绍了Hexo的配置，以及发布到GitHub上

[Hexo的基本配置]: http://www.azxcvb.cn/2019/01/07/Hexo%E5%9F%BA%E6%9C%AC%E9%85%8D%E7%BD%AE/	"Hexo"

这篇进行将博客地址连接到阿里云服务器的域名上

将username.github.io地址改为自己服务器的域名地址

username.github.io ==> http://www.azxcvb.cn/

#### 一、阿里云配置

配置域名解析

![阿里云](aly.png)

需要注意：

配置时username.github.io. 后面的.

这个是直接配置在主域名下边的，二级域名的话将www和@改为二级域名的地址



#### 二、配置Hexo

##### 1、修改index.html文件

将Hexo根目录下的index.html打开，修改为如下

![hexo](hexo.png)

##### 2、增加CNAME文件

在根目录下增加CNAME文件，没有后缀，大写

文件中写上自己的域名azxcvb.cn  **不用写http://、 www**

##### 3、推送并重新部署Hexo

将修改git push到GitHub上

进行

```
hexo clean
hexo deploy
```

#### 三、配置GitHub

进入博客仓库的page界面，找到setting界面

![setting](set.png)

找到Custom domain，将域名填写到这里保存www.azxcvb.cn

![custom](cus.png)

通过http://www.azxcvb.cn/ 就可以访问之前的username.github.io界面



