---
title: 阿里云域名配置以及https证书（ssl证书）配置
date: 2019-01-06 15:07:07
tags: "Https"
categories: "服务器"
---

### 阿里云域名配置以及https证书配置

​        开发小程序，小程序开发使用的所有接口都必须是https的，然后申请了阿里云服务器，申请注册域名，普通域名一年差不多20块多点
进入域名控制台，点击添加纪录，进行增加以下*/www/@这三个，记录值为要绑定域名的IP地址（服务器对应的外网IP），保存就好

![在这里插入图片描述](https://img-blog.csdn.net/20181014093009192?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTMwMDk4MDg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
配置好之后，之前通过http://XX.XX.XX.XX:8080访问的地址可以通过http://域名:8080访问

**开始配置HTTPS**
在阿里云搜索框中进行搜索**ssl证书**
点击进入
![在这里插入图片描述](https://img-blog.csdn.net/2018101409361533?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTMwMDk4MDg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
点击立即购买
选择以下这几个选项，有**免费**的，只是安全性差点，点击购买
![在这里插入图片描述](https://img-blog.csdn.net/20181014100037108?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTMwMDk4MDg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
再次进入控制台就会看到以下实例，不过状态这里是没有签发，需要补全信息，进行审核，信息不是很多，审核很快的，基本上30分钟之内
![在这里插入图片描述](https://img-blog.csdn.net/20181014100109827?0000000watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTMwMDk4MDg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

配置完之后，点击后边下载，
![在这里插入图片描述](https://img-blog.csdn.net/20181014100134499?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTMwMDk4MDg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
选择自己的服务器，我这里配置的是tomcat

##### 一、配置tomcat的https

​        可以按照说明进行配置，PFX和JKS只用安装一个就可以了
下载完证书，在tomcat中创建文件夹为cert，将文件解压后放在cret中
以下是我的配置文件
在tomcat的server.xml中增加：

```
<Connector port="443" protocol="HTTP/1.1"
               maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
			   clientAuth="false" sslProtocol="TLS" keystoreFile="cert/21506440638****.pfx" keystorePass="2150644063******"
			   >
```

**将端口8443更改为443**

在tomcat的web.xml的<welcome-file-list>标签后增加以下代码

```
	<login-config> 
	<!-- Authorization setting for SSL --> 
		<auth-method>CLIENT-CERT</auth-method> 
		<realm-name>Client Cert Users-only Area</realm-name> 
	</login-config> 
	<security-constraint> 
		<!-- Authorization setting for SSL --> 
		<web-resource-collection > 
		<web-resource-name >SSL</web-resource-name> 
		<url-pattern>/*</url-pattern> 
		</web-resource-collection> 
		<user-data-constraint> 
		<transport-guarantee>CONFIDENTIAL</transport-guarantee> 
		</user-data-constraint> 
	</security-constraint>
```

然后重启tomcat服务器
地址访问：Https://域名/项目

##### 二、配置nginx的https

一个服务器下配置多个域名访问
只有一个服务器，然后需要配置小程序以及其它项目的后台
在nginx进行监听443端口，然后进行域名转发

```
server{
        listen 443 ssl; #监听443端口
        server_name online2.XXXX.cn;#域名
        index index.html index.htm; #访问首页地址
		root D:\wx_address_tomcat\webapps\spring_70_s4s2h5_03;
        ssl_certificate "D:/nginx2/nginx-1.15.1/cert/1648469_online2.XXXX.cn.pem";
        ssl_certificate_key  "D:/nginx2/nginx-1.15.1/cert/1648469_online2.XXXX.cn.key";#对应的证书key文件路径
		ssl_protocols TLSv1 TLSv1.1 TLSv1.2;		
        location  / {
			proxy_pass http://localhost:8020; #对应监听的接口，转发的地址
		}
	}		
server{
        listen 443 ssl; #监听443端口
        server_name online2.DDDD.cn;#域名
        index index.html index.htm; #访问首页地址
		root D:\wx_address_tomcat\webapps\spring_70_s4s2h5_03;
        ssl_certificate "D:/nginx2/nginx-1.15.1/cert/1648469_online2.DDDD.cn.pem";
        ssl_certificate_key  "D:/nginx2/nginx-1.15.1/cert/1648469_online2.DDDD.cn.key";#对应的证书key文件路径
		ssl_protocols TLSv1 TLSv1.1 TLSv1.2;		
        location  / {
			proxy_pass http://localhost:8888; #对应监听的接口，转发的地址
		}
		location /resources/ {
           **alias D:/apache-tomcat-7.0.59_64/XXXX/ROOT/resources/;#重命名到nginx目录下,直接由nginx提供,不经过tomcat,所以你们要拷贝或者直接剪切静态资源到这边**
           	expires 1d; #文件缓存时间1天,前端会收到这个
        }
	}	
```

访问的时候就可以根据不同的域名进行访问了
静态文件对应的地址：
如果访问的路径中包含resources/，则会跳转到具体的静态文件路径中
访问的地址为：http://online2.DDDD.cn/resources/image.png 就可以访问具体的文件了