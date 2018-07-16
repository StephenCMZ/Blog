---
title: 第一个Flutter应用程序
date: 2018-07-15 21:37:14
categories:
- Flutter
---

`Flutter` 是 Google 用以帮助开发者在 iOS 和 Android 两个平台开发高质量原生 UI 的移动 SDK。Flutter 兼容现有的代码，免费且开源，在全球开发者中广泛被使用。

这段时间国内的许多开发者已经开始高度关注`Flutter`，由于它提供了另外一种高效的跨平台解决思路，同时还提供了高质量的UI，这是移动开发者一个极大的便利，也是值得让移动开发者兴奋的事情。

`Flutter`采用的开发语言是`Dart`,可能很多开发者都不是很了解这个语言，因为在之前我们使用的地方也确实不多。`Dart`也是Google的产品，有其他面向对象语言基础的开发者基本上是可以无缝使用的，个人觉得使用起来很舒服。

本文就先从开发环境的搭建开始，一步步创建第一个Flutter应用。

### 主要内容如下：
1. Windows下Flutter开发环境的搭建
2. 创建第一个Flutter应用
3. 介绍Flutter应用的目录结构
4. 介绍Flutter应用的代码

### 在开始之前，先列举几个不错的Flutter学习站点：
1. Flutter官网  [https://flutter.io/](https://flutter.io/)
2. Flutter中文官网  [https://flutter-io.cn/](https://flutter-io.cn/)
3. 咸鱼技术 [https://yuque.com/xytech/flutter](https://yuque.com/xytech/flutter)
4. Dart语言官网 [https://www.dartlang.org/](https://www.dartlang.org/)

### Windows下Flutter开发环境的搭建：

Flutter的环境搭建比较简单，只需要根据官方的文档一步步进行便可以了，具体如下：

1. 下载[FlutterSDK](https://storage.googleapis.com/flutter_infra/releases/beta/windows/flutter_windows_v0.5.1-beta.zip)，并解压到任意路径下，我们为了使用的方便，同时将FlutterSDK路径添加到Windows的环境变量中：

	![](/images/flutter/FlutterSDK.PNG)
	> 这里解压到`D:\ProgramFiles\flutter`中，值得注意的是，路径中不能存在空格，当然最好也不要存在中文

	![](/images/flutter/FlutterHome.PNG)
	> 将FlutterSDK路径添加到系统的环境变量Path中

2. 使用AndroidStudio作为开发IDE，当然也可以使用VSCode作为开的IDE。我们为AndroidStudio添加Flutter开发的相关插件：
	
	![](/images/flutter/FlutterPlugin.PNG)
	> 在AndroidStudio中，找到菜单`Setting`->`Plugins`->`Browse repositories`， 然后搜索`Flutter`，便会出现flutter的插件，点击安装，这个时候会提醒有一个`Dart`依赖插件，继续点击安装即可。安装完成后，我们需要重启一下AndroidStudio才能使插件生效

3. 使用FlutterDoctor检查开发环境：
	
	![](/images/flutter/FlutterDoctor.PNG)
	> FlutterDoctor是Flutter提供给我们的环境检查工具，我们在windows中打开cmd，输入`flutter doctor`, 此时便会列举我们系统当前的Flutter环境。如果在某一项没有提示`[√]`，说明该项存在问题，只需要根据提示输入命令修复一下即可

### 创建第一个Flutter应用：

使用AndroidStudio创建Flutter项目具体如下：

![](/images/flutter/FlutterStart.png)
> 在AndroidStudio中选择`Start a new Flutter project`开始创建应用
	
![](/images/flutter/FlutterNext.png)
> 填写一些应用环境及相关的信息，点击`Next`
	
![](/images/flutter/FlutterCompany.png)
> 填写公司标识，点击`Finish`，稍等片刻即可完成项目的创建

### 介绍Flutter应用的目录结构：
![](/images/flutter/FlutterFolder.png)
> 如上图所示，flutter创建好的目录结构非常简洁
> `android`目录包含了Andorid项目的文件，和我们正常创建的Android项目差不多
> `ios`目录包含iOS项目的文件，采用的是Pod管理项目
> `lib`便是我们放置Flutter应用源码的目录
> `pubspec.yaml`是Flutter项目依赖的配置文件，这个文件比较重要，我们会经常使用到


### 介绍Flutter应用的代码：
    import 'package:flutter/material.dart';

	void main() => runApp(new MyApp());
	
	// MyApp组件
	class MyApp extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return new MaterialApp(
	      title: 'Flutter Demo',
	      theme: new ThemeData(
	        primarySwatch: Colors.blue,
	      ),
	      home: new MyHomePage(title: 'Flutter Demo Home Page'),
	    );
	  }
	}
	
	// MyHomePage组件
	class MyHomePage extends StatefulWidget {
	  MyHomePage({Key key, this.title}) : super(key: key);
	  final String title;
	
	  @override
	  _MyHomePageState createState() => new _MyHomePageState();
	}
	
	// MyHomePage组件的State
	class _MyHomePageState extends State<MyHomePage> {
	  int _counter = 0; //当前计数
	
	  //计数方法
	  void _incrementCounter() {
	    setState(() {
	      _counter++; //计数自增加一
	    });
	  }
	
	  //组件的构建方法
	  @override
	  Widget build(BuildContext context) {
	    return new Scaffold(
	      appBar: new AppBar( //菜单栏组件
	        title: new Text(widget.title), //文本组件
	      ),
	      body: new Center( //居中组件
	        child: new Column( //列组件
	          mainAxisAlignment: MainAxisAlignment.center, //主轴居中
	          children: <Widget>[
	            new Text( //文本组件
	              'You have pushed the button this many times:',
	            ),
	            new Text( //文本组件
	              '$_counter',
	              style: Theme.of(context).textTheme.display1,
	            ),
	          ],
	        ),
	      ),
	      floatingActionButton: new FloatingActionButton( //浮动按钮组件
	        onPressed: _incrementCounter,
	        tooltip: 'Increment',
	        child: new Icon(Icons.add),
	      ),
	    );
	  }
	}

> 在新建的项目中，Flutter已经为我们添加了`main.dart`文件，实现了一个简单的Demo，这里稍微介绍一下
> 从注释可以看到，这个Demo由很多的`组件`组成，是的，在Flutter中，组件是一个非常重要的概念，我们可以把它理解为一个个元素
> 程序从`main`方法开始，在该方法中创建了一个没有中间状态的`MyApp`，即`StatelessWidget`的子类`MyApp`
> `MyApp`中配置了App的名称`title`和主题颜色`primarySwatch`, 同时创建了带中间状态的`MyHomePage`，即`StatefulWidget`的子类`MyHomePage`
> 在`MyHomePage`的状态`_MyHomePageState`中，使用了`_counter`字段记录了当前的计数，同时在`_incrementCounter`方法中，通过`setState`方法修改计数，从而使被修改的计数同时更新到UI上
> `_MyHomePageState`的构建比较简单，总体的布局是列布局，所以使用了`Column`组件，在该组件中有两个文本，一个显示提示说明，另外一个用于显示当前计数。除了列布局外，在顶层还添加了一个悬浮按钮`floatingActionButton`，悬浮按钮事件便是`_incrementCounter`，当点击按钮时，便会触发计数事件，使计数增加同时更新到UI上

具体的运行效果如下：
![](/images/flutter/FlutterRun.png)

第一个Flutter应用程序就介绍到这里，如果有兴趣可以扫码加入微信群，大家一起交流学习。
<img src="/images/flutter/FlutterGroup.jpg" width="25%" hegiht="25%" div align=center />