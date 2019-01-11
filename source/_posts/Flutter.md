---
title: Flutter
date: 2019-01-11 15:24:43
tags: Flutter
categories: 
- Flutter
- Flutter基础
---

### Flutter基础知识

##### 1、开始Hello

编写hello

```
import 'package:flutter/material.dart'; //导入
void main() => runApp(MyApp()); 
class MyApp extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      home: Scaffold(
        appBar: new AppBar(
          title: new Text("测试Flutter"),
        ),
        body: new Text("Hello Flutter"),
      ),
    );
  }
}
```

运行的效果

![hello](hello.png)

##### 2、文本的使用

文本的样式

文本下划线

文本对齐方式

```
import 'package:flutter/material.dart';

void main()=>runApp(MyApp());

class MyApp extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      home: Scaffold(
        appBar: new AppBar(
          title: new Text("测试Flutter"),
        ),
        body: Text(
          "Flutter是谷歌的移动UI框架，可以快速在iOS和Android上构建高质量的原生用户界面。 Flutter可以与现有的代码一起工作。在全世界，Flutter正在被越来越多的开发者和组织使用，并且Flutter是完全免费、开源的。",
          textAlign: TextAlign.left, //对齐方式
//        maxLines: 1, //最大显示几行
//        overflow: TextOverflow.clip, //文本超出显示方式clip 默认 ellipsis 超出... fade 模糊
          style: TextStyle(
              fontSize: 25.0, //字体大小
              color: Colors.lightBlue, //颜色Color.fromARGB(255, 255, 150, 150)或者Colors.lightBlue
              decoration: TextDecoration.underline, //下划线
              decorationStyle: TextDecorationStyle.solid //实线 还有其他样式
          ),
        ),
      ),
    );
  }
}
```

![text](text.png)

##### 3、图片使用

```
import 'package:flutter/material.dart';

void main() => runApp(MyApp());
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text("Hello World"),
        ),
        body: Center(
          child: Container(
            child: new Image.network(
              'https://img1.sycdn.imooc.com/5c106ea20001505b18720632.jpg',
              scale: 5.0, //缩放
//              fit: BoxFit.fitHeight, //充满图片fill 保存比例充满cover
//              color: Colors.red,
//              colorBlendMode: BlendMode.darken, //图片叠加模式
              repeat: ImageRepeat.repeatX, //重复
            ),
            width: 400.0,
            height: 300.0,
            color: Colors.lightBlue,
          )
        ),
      )
    );
  }
}
```

![image](image.png)

