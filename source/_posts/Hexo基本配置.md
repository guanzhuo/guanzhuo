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

如果出现Could not open a connection to your authentication agent

在c盘下找到.ssh文件夹，cmd进入到该层目录（C:\Users\Administrator\.ssh）输入：

```
ssh-agent bash
```

如果提示

```
unable to start ssh-agent service, error :1058
```

在计算机服务中，找到OpenSSH Authentication Agent 服务，将禁用更改为手动或者自动，启动该服务，即可

再执行

```
ssh-add id_rsa
```

![git_add](gitadd.png)

将密钥配置到GIT ssh中

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

##### 4、创建文件夹

```
npm install
#安装hexo
#可以更换淘宝镜像
#npm config set registry https://registry.npm.taobao.org
#验证  输入 npm config get registry
#输出 https://registry.npm.taobao.org/ 镜像更换好了
npm install hexo -g
npm install hexo -server --save
hexo init
```

输入

```
hexo server
```

本地访问 localhost:4000 即可

##### 5、配置hexo到Git

部署到Git 之前，需要安装

```
npm install hexo-deployer-git --save
```



##### 6、修改配置信息

仓库地址：Repo

![repo](repo.png)

##### 7、编译部署

新建  hexo new “gz测试”

hexo clean    重新编译

hexo deploy    重新部署

使用 https://guanzhuo.github.io/ 访问

