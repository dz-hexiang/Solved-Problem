---
title: adb常用命令
date: 2017-11-21 17:36:17
tags:
---
1.把日志打印出来

```
adb logcat -d > logcat.txt
```

2.把手/sdcard/Screenshots/下面的照片全部复制到 screenshots目录下

```
adb pull /sdcard/Screenshots/ screenshots\.
```

3.把文件复制到 手机sd卡根目录上 (开机动画)

```
adb push bootanimation.zip /mnt/sdcard/
```

4.把文件复制到 手机sd卡根目录上 (关机动画)

```
adb push shutanimation.zip /mnt/sdcard/
```

5.关掉adb

```
adb kill-server
```

6.重启adb

```
adb start-server
```

7.查看识别的设备

```
adb devices
```
```