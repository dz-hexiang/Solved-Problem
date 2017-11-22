---
title: 如何使用JDK中的keytool工具获取keysotre签名里面的信息
date: 2017-11-21 17:36:17
tags:
---
##### 如何使用JDK中的keytool工具获取keysotre签名里面的信息
1.把下面的命令输入到cmd界面中，按回车（ keystore.keystor是签名文件）

    keytool -list -v -keystore keystore.keystore

2.输入签名文件密码回车即可，如图
![这里写图片描述](http://img.blog.csdn.net/20171120170929183?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZHpfaGV4aWFuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)