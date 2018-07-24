---
title: 在Android工程中添加Flutter模块
date: 2018-07-24 13:58:06
categories:
- Flutter
---

在新建好的Flutter项目中，我们发现Flutter和Android或iOS原生项目混合得分不开，那么我们该如何在原有的Android项目中进入Flutter呢？

#### 步骤还是比较简单的，如同把大象放入冰箱里，只需要3步：
1. 创建Android原生项目
2. 创建Flutter模块
3. 在原生Android项目中添加Flutter模块依赖

#### 1. 创建Android原生项目

这一步骤其实没有什么好说的了，就是我们原来创建一个Android原生项目
这里就创建一个项目叫做`MyApp`

#### 2. 创建Flutter模块

在上一步创建好的MyApp工程的同级目录下，注意不是MyApp工程的根目录，运行以下命令：
```
$ flutter create -t module my_flutter
```
这个命令的意思是，创建一个`module`模块名称为`my_flutter`

这里可能会因为我国网络的原因创建非常慢，解决的办法就是添加国内镜像路径到系统的环境变量中，以下是两个镜像，选择其一添加即可：
```
上海交通大学 Linux 用户组
FLUTTER_STORAGE_BASE_URL: https://mirrors.sjtug.sjtu.edu.cn
PUB_HOSTED_URL: https://dart-pub.mirrors.sjtug.sjtu.edu.cn

Flutter 社区
FLUTTER_STORAGE_BASE_URL: https://storage.flutter-io.cn
PUB_HOSTED_URL: https://pub.flutter-io.cn
```

#### 3. 在原生Android项目中添加Flutter模块依赖

添加依赖需要做两步，第一就是把模块引入到工程中，第二步便是添加模块依赖了，具体如下：

1. 在`MyApp`工程中的`settings.gradle`文件中添加如下代码：
``` 
setBinding(new Binding([gradle: this]))
evaluate(new File(
        settingsDir.parentFile,
        'my_flutter/.android/include_flutter.groovy'
))
```
2. 在工程中`App`的`build.gradle`中添加`dependencies`，注意这里不是工程的`build.gradle`:
```
implementation project(':flutter')
```

至此，我们已经完成了在Android工程中添加Flutter模块。

如果此时点击AndroidStudio的运行按钮，并没有报错，那么恭喜你，运气真好。但是我运气并没有那么好，在过程中还是遇到了一些小问题：

#### 遇到的一些问题
1. 提醒SDKTools,版本不对，无法编译，解决方法是在Flutter模块的`build.gradle`中将其替换成为正确的版本，如下：
```
//替换前
dependencies {
    testImplementation 'junit:junit:4.12'
    implementation 'com.android.support:support-v13:27.0.3'
    implementation 'com.android.support:support-annotations:27.0.3'
}

//替换后
dependencies {
    testImplementation 'junit:junit:4.12'
    implementation 'com.android.support:appcompat-v7:28.0.0-alpha3'
    implementation 'com.android.support:appcompat-v7:28.0.0-alpha3'
}
```
这里替换的是当前本地的SDKTools版本，这个版本号可以在`App`的`build.gradle`中查看，直接复制过来即可

2. 完成以上替换后，AndroidStudio再次提醒AndroidSdk版本号不匹配，解决方法还是在Flutter模块的`build.gradle`中将其替换成为正确的版本，如下：
```
// 替换前
android {
    compileSdkVersion 27

    defaultConfig {
        minSdkVersion 16
        targetSdkVersion 27
        ...
    }
}

//替换后
android {
    compileSdkVersion 28

    defaultConfig {
        minSdkVersion 16
        targetSdkVersion 28
        ...
    }
}
```

3. minSdkVersion不匹配，好吧，还是版本号的问题，不过这次是App模块的`build.gradle`，替换如下：
```
// 替换前
android {
    compileSdkVersion 28
    defaultConfig {
        minSdkVersion 15
        ...
    }
}

//替换后
android {
    compileSdkVersion 28
    defaultConfig {
        minSdkVersion 16
        ...
    }
}
```
这里有个小的建议，就是尽可能地将各个模块中的`compileSdkVersion`,`minSdkVersion`等各种版本号替换为一致，避免出现一些奇怪的问题，当然最好是能在外部定义一个文件统一管理，然后在各个模块中的`build.gradle`进行引用。

#### 源码
```
https://github.com/StephenCMZ/flutter_hybrid
```

#### 参考

```
https://github.com/flutter/flutter-intellij
https://zhuanlan.zhihu.com/p/40373247
```