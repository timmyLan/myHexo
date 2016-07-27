---
title: react-native-android-test
date: 2016-07-19 18:49:51
categories:
- react
tags:
- react
- native
- android
- debug
---
react-native Android 真机测试
=================================

我并不喜欢吐槽，但系理论上虚拟机上跑起的程序到真机不可以开飞机？然而:( 我还是图样图森破

———————————————————————————————————————————————————————————————————————吐槽分割线
真机测试遇到的bug
----------------------------
1.
```bash
:app:installDebug FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:installDebug'.
> com.android.builder.testing.api.DeviceException: com.android.ddmlib.InstallException:  Unable to upload some APKs
...
```
解决方案: 将{YourProduct}\android\build.gradle 改成
{% codeblock lang:js %}
...
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:1.2.3'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
...
{% endcodeblock%}

2.解决上述问题再跑react-native run-android，红色error界面 提示`Unable to download JS bundle`
解决方案：
```bash
adb reverse tcp:8081 tcp:8081
react-native run-android
```
3.测试界面出来了，与虚拟机的一模一样，弹出开发者菜单
```bash
#摇一摇:) 使劲摇 or
adb shell input keyevent 82
```
点击`Enable Hot Reloading`，改改index.android.js代码，红色error界面
解决方案：
- 查出本机内网ip{%link 百度方法 http://jingyan.baidu.com/article/154b46315814a928ca8f41d7.html%}
- 弹出开发者菜单->Dev Settings->Debug server host & port for device
- 输入本机ip:8081

真机测试结果
-------------------------
{% asset_img finish.png finish%}
