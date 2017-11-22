---
title:android-studio Android Duplicate files copied in APK
date: 2014-11-21 17:36:17
tags:
---
#### Duplicate files copied in APK META-INF/DEPENDENCIES File 1: httpmime-4.3.2.jar File 2: httpmime-4.3.2.jar     
##### 解决办法，打开项目下面的 build.gradle 文件，在 android 代码块中添加下面代码

```
android {  
    packagingOptions {  
        exclude 'META-INF/DEPENDENCIES'  
        exclude 'META-INF/NOTICE'  
        exclude 'META-INF/LICENSE'  
        exclude 'META-INF/LICENSE.txt'  
        exclude 'META-INF/NOTICE.txt'  
    }  
}  
```