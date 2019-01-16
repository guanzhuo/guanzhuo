---
title: Hexo更换Git仓库（GitHub更换为Coding）
date: 2019-01-16 14:56:53
tags: Hexo
categories: Hexo
---

#### Hexo更换Git仓库（GitHub更换为Coding）

更换git仓库同时将Hexo部署到两个代码仓库中

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

