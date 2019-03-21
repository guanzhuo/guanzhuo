---
title: Redis在阿里云服务器Centos上的配置
date: 2019-03-21 09:21:08
tags:
---

#### Redis在阿里云服务器Centos上的配置

1、安装

安装Redis

需要安装gcc-c++

```
yum install gcc-c++
```

下载Redis的压缩包，将文件传到Centos上（可以使用FileZilla），或者直接下载

```
$ wget http://download.redis.io/releases/redis-5.0.4.tar.gz 
```

进行解压

```
tar -zxvf redis-5.0.4.tar.gz
```

编译

```
$ make
$ make install PREFIX=/usr/local/redis //安装到/usr/local/redis中
$ make test //检查Redis是否编译正确
```

运行：

进入安装目录/usr/local/redis/bin

```
./redis-server
```

2、配置

将redis.conf拷贝到安装目录

vim redis.conf

查找的方法：在没有编辑的状态下，输入/bind，回车，搜索bind.查看下一个是n

查找bind:127.0.0.1 -->0.0.0.0

修改daemonize no -->yes

取消密码注释：requirepass root -->修改密码

退出：ESC-->:wq

运行：

```
./redis-server redis.conf
```

3、连接测试

输入，root为密码

```
./redis-cli -p 6379 -a root
输入set hello helloworld
```

<div align=center>
    <img width=300 src='https://gzsave.oss-cn-shenzhen.aliyuncs.com/redis/redis1.png'/>
</div>

然后get hello，输出helloworld.

安装完成

4、远程连接

使用systemctl stop firewalld.service 关闭防火墙

firewall-cmd --state 查看防火墙状态

然后就可以使用Redis Desktop Manager进行连接

