---
title: 小程序开发--swagger2
date: 2019-03-16 11:10:09
tags: 开发工具
categories: swagger2
---

##### swagger2使用

使用swagger2构建restful接口测试

1、可以生成文档形式的api并提供给不同的团队

2、便于自测

3、无需过多冗余的word文档



配置，需要在后台的pom.xml中进行增加配置文件

```xml
<!-- swagger2配置 -->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.4.0</version>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.4.0</version>
</dependency>
```



