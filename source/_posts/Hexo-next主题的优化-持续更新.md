---
title: Hexo next主题的优化(持续更新...)
date: 2019-01-03 14:40:38
tags: "Hexo"
categories: "Hexo"
---

#### Hexo next主题的优化(持续更新...)

##### 1.首页显示概览

找到目录 -- hexo->themes/next ->config.yml 

搜索auto_excerpt

修改如下：

![auto](auto_excerpt.png)

将enable改为true即可

##### 2.设置头像

![setIcon](setIcon.png)

头像的地址：themes\next\source\images

##### 3.增加点击弹出小红心

在如下地址中：themes\next\source\js\src

增加clicklove.js文件，内容如下：

```js
!function(e,t,a){function n(){c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),o(),r()}function r(){for(var e=0;e<d.length;e++)d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");requestAnimationFrame(r)}function o(){var t="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){t&&t(),i(e)}}function i(e){var a=t.createElement("div");a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)}function c(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}function s(){return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}var d=[];e.requestAnimationFrame=function(){return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)}}(),n()}(window,document);
```

在\themes\next\layout\_layout.swig文件末尾添加

<!-- 页面点击小红心 -->

<script type="text/javascript" src="/js/src/clicklove.js"></script>

![click](click.png)

##### 4.添加动图

安装：npm install --save hexo-helper-live2d

修改配置文件（站点的配置文件）

文末增加：

```xml
live2d:
      enable: true
      scriptFrom: local
      model:
        scale: 1
        hHeadPos: 0.5
        vHeadPos: 0.618
      display:
        superSample: 2
        width: 150
        height: 300
        position: right
        hOffset: 0
        vOffset: -20
      mobile:
        show: false
      react:
        opacityDefault: 0.5
        opacityOnHover: 0
```

即可

##### 5.去掉系统的目录，使用自己的目录

去点之前

![旧](mulu.png)

去掉之后

![新](mulnNew.png)

修改

![](2.png)

number设置为false即可