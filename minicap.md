安装minicap与minitouch：

<https://blog.csdn.net/s1162276945/article/details/80870389>

Minicap:

<https://blog.csdn.net/zhonglunshun/article/details/80831537>

<https://www.cnblogs.com/qiangayz/p/9580389.html>

 

两篇很好的文章：

Minicap：

<https://testerhome.com/topics/3115>

Minitouch：

<https://testerhome.com/topics/4400>

Pyminitouch：

<https://testerhome.com/topics/17410>

 

 

 

 

 

Minicap 启动流程：（手机端建立服务器）

cd minicap

ABI=$(adb shell getprop ro.product.cpu.abi)

ndk-build.cmd APP_PLATFORM=android-25 APP_ABI=ABI

adb push libs/$ABI/minicap /data/local/tmp/

SDK=$(adb shell getprop ro.build.version.sdk)

adb push jni/minicap-shared/aosp/libs/android-$SDK/$ABI/minicap.so /data/local/tmp/

adb forward tcp:1717 localabstract:minicap

adb shell wm size

adb shell LD_LIBRARY_PATH=/data/local/tmp /data/local/tmp/minicap -P 1080x2160@1080x2160/0

 

客户端搭建：

代码： Minicap.py (py27)

简书：pyqt渲染

<https://www.jianshu.com/p/777af34b4f21>

Minitouch

 

DeviceId 获取

Adb devices

 

46d90681

有时候 报错，说端口被占用，是因为上次使用了手机设备没有stop，再次插拔一下手机就可以了