---
title: Hexo更换Git仓库（GitHub更换为Coding）
date: 2019-01-16 14:56:53
tags: Hexo
categories: Hexo
---

#### Hexo更换Git仓库（GitHub更换为Coding）

更换git仓库同时将Hexo部署到两个代码仓库中

##### 1、_config.yml配置

修改Hexo的配置文件

```
  repo: 
    github: git@github.com:guanzhuo/guanzhuo.git
    coding: git@git.dev.tencent.com:azxcvb/blog.git
```

格式一定要正确

修改url地址：

```
url: https://www.azxcvb.cn
root: /
#url: http://azxcvb.coding.me/blog/ #如果单独在coding上显示，使用该地址，同时root为/blog
```

2、coding上新建项目

3、设置公钥，方法跟GitHub相同

参考 

[Hexo的基本配置]: http://www.azxcvb.cn/2019/01/07/Hexo%E5%9F%BA%E6%9C%AC%E9%85%8D%E7%BD%AE/	"Hexo"

##### 1、代码更新到最新

```
git add .
git commit -m "***"
git push
git pull
git status #查看状态
```

##### 2、删除.git文件夹

##### 3、重新绑定

```
git init
git remote add origin git@git.coding.net:...
git add .
git commit -m "***"
git push -u origin master 
```

