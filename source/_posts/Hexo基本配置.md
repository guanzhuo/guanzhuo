---
title: Hexo基本配置
date: 2019-01-07 09:21:36
tags: Hexo
categories: Hexo

---

#### Hexo的基本配置

hexo的基本配置

##### 1、安装 Git

推荐网址：http://www.bootcss.com/p/git-guide/ 这个网指南不错，而且是中文的，介绍的很详细

##### 2、安装 node

推荐网址：http://www.runoob.com/nodejs/nodejs-install-setup.html

进行安装node

##### 3、生成 Key

```
ssh-keygen -t rsa -C "username@qq.com"
```



![key](key.png)

```
$ ssh-add ~/.ssh/id_rsa

（找不到文件再使用）ssh-agent bash
```

![load](load.png)

##### 4、创建文件夹

```
hexo init
npm install
npm install hexo -server --save
```

输入

```
hexo server
```

本地访问 localhost:4000 即可

##### 5、配置到GIT

```
npm install hexo-deployer-git --save
```

Git 上设置密钥

![git](git.png)

查看密钥是否成功

```
ssh -T git@github.com
```

![res](res.png)

同时Git上这两个地方也需要修改

![git](git1.png)

![git](git2.png)

##### 6、修改配置信息

仓库地址：Repo

![repo](repo.png)

##### 7、编译部署

新建  hexo new “gz测试”

hexo clean    重新编译

hexo deploy    重新部署

使用 https://guanzhuo.github.io/ 访问

