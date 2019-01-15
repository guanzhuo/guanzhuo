---
title: Flutter
date: 2019-01-11 15:24:43
tags: Flutter
categories: 
- Flutter
- Flutter基础
---

### Flutter基础知识

#### 1、开始Hello

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

#### 2、文本的使用

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

#### 3、图片使用

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

#### 4、滚动水平进行滑动

```
import 'package:flutter/material.dart';

void main() => runApp(MyApp(
  items:new List<String>.generate(1000, (i)=>"Item $i") //构造器gen
));

class MyApp extends StatelessWidget {
  final List<String> items;
  MyApp({Key key,@required this.items}):super(key:key);
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'GGGZZZ',
      home: Scaffold(
          appBar: new AppBar(
            title: new Text("ListText"),
          ),
          body: Center(
            child: Container(
              height: 200.0,
              child: new MyList(),
            ),
          )
          ),
    );
  }
}
class MyList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new ListView(
      scrollDirection: Axis.horizontal, //滚动方向
      children: <Widget>[
        new Container(
          width: 180.0,
          color: Colors.lightBlue,
        ),
        new Container(
          width: 180.0,
          color: Colors.red,
        ),
        new Container(
          width: 180.0,
          color: Colors.brown,
        ),
        new Container(
          width: 180.0,
          color: Colors.amberAccent,
        ),
      ],
    );
  }
}
```

效果

![list](list.png)

#### 5、整体滑动

```
import 'package:flutter/material.dart';

void main() => runApp(MyApp());
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: '电影实例测试',
      home: Scaffold(
        appBar: AppBar(
          title: new Text("电影==="),
        ),
        body: GridView(
          gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
              crossAxisCount: 3,
            mainAxisSpacing: 5.0,
            crossAxisSpacing: 5.0,
            childAspectRatio: 0.7, //长宽比
          ),
          children: <Widget>[
            new Image.network("http://img5.mtime.cn/mg/2018/12/24/092753.17665902_126X190X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mg/2018/12/27/153235.18379383_126X190X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mg/2018/12/29/205103.16573451_126X190X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mt/2019/01/04/212012.14279509_100X140X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mg/2018/12/24/092753.17665902_126X190X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mg/2018/12/27/153235.18379383_126X190X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mg/2018/12/29/205103.16573451_126X190X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mt/2019/01/04/212012.14279509_100X140X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mg/2018/12/24/092753.17665902_126X190X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mg/2018/12/27/153235.18379383_126X190X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mg/2018/12/29/205103.16573451_126X190X4.jpg",fit: BoxFit.cover,),
            new Image.network("http://img5.mtime.cn/mt/2019/01/04/212012.14279509_100X140X4.jpg",fit: BoxFit.cover,),
          ],
        )
      ),
    );
  }
}
```

滑动效果

![movie](movie.png)

#### 6、底部导航栏

##### 1、新建界面

navigation.dart (first.dart  second.dart  third.dart三个界面)

![lib](lib.png)

##### 2、navigation.dart

```
import 'package:flutter/material.dart';
import 'package:flutter_t/first.dart';
import 'package:flutter_t/second.dart';
import 'package:flutter_t/third.dart';
void main(){
  runApp(new MyApp());
}
class MyApp extends StatefulWidget{
  @override
  State<StatefulWidget> createState() {
    return new _MyHomeState();
  }
}
class _MyHomeState extends State<MyApp> with TickerProviderStateMixin{
  int _tabIndex = 0;
  List<BottomNavigationBarItem> _navViews;
  var appBarTitles = ['首页','发现','我的'];
  PageController pageController;
  var body;
  initData(){
    body = new IndexedStack(
      children: <Widget>[new First(),new Second(),new Third()],
      index: _tabIndex,
    );
  }
  @override
  void initState() {
    super.initState();
    _navViews = <BottomNavigationBarItem>[
      new BottomNavigationBarItem(
        icon: const Icon(Icons.home),
        title: new Text(appBarTitles[0]),
        backgroundColor:Colors.lightBlue
      ),
      new BottomNavigationBarItem(
          icon: const Icon(Icons.find_replace),
          title: new Text(appBarTitles[1]),
          backgroundColor:Colors.lightBlue
      ),
      new BottomNavigationBarItem(
          icon: const Icon(Icons.person),
          title: new Text(appBarTitles[2]),
          backgroundColor:Colors.lightBlue
      ),
    ];
  }
  
  final navigatorKey = GlobalKey<NavigatorState>();
  @override
  Widget build(BuildContext context) {
    initData();
    return new MaterialApp(
      navigatorKey: navigatorKey,
      theme: new ThemeData(
        primaryColor: Colors.lightBlue,
        accentColor: Colors.lightBlue
      ),
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text(
            appBarTitles[_tabIndex],
            style: new TextStyle(color: Colors.red),
          ),
        ),
        body: body,
        bottomNavigationBar: new BottomNavigationBar(
          items: _navViews.map((BottomNavigationBarItem navView)=>navView).toList(),
          currentIndex: _tabIndex,
          type: BottomNavigationBarType.fixed,
          onTap: (index){
            setState(() {
              _tabIndex = index;
            });
          },
        ),
      ),
    );
  }
}
```

##### 3、其他三个界面的代码基本相同

```
import 'package:flutter/material.dart';

class First extends StatefulWidget{
  @override
  State<StatefulWidget> createState() {
    return null;
  }
}
class FirstState extends State<First>{
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      body: new Center(
        child: new Text("第一个界面"),
      ),
    );
  }
}
```

![find](find.png)

![index](index.png)



