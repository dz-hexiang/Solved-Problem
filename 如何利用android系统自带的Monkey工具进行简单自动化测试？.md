#如何利用android系统自带的Monkey工具进行简单自动化测试？
##一、首先是配置adb环境
adb命令就是Android SDK中的platform-tools下的adb.exe ,可以把platform-tools像配置jdk一样配置到环境变量中，cmd中就可以直接敲adb命令了


##二、通过adb命令使用monkey工具
下面三个命令是在cmd命令行中执行
###1.进入shell环境
adb shell  
###2.进入程序安装目录
cd /data/data  
###3.敲入monkey 命令就可以测试安装包 （其他一些模拟事件可以去网上搜搜）
###它启动指定的应用程序，并向其发送1000个伪随机事件

monkey -p com.bonade.xxp.test -v 1000   