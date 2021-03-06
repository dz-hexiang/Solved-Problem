---
title: dep和rpm的安装
date: 2015-7-21 17:36:17
tags:
---
#### 一、deb 是 ubuntu 、debian 的格式,是debian发行版的软件包,ubuntu是基于debian 发行的 所有可以用。
dpkg 是Debian Package的简写，是为Debian 专门开发的套件管理系统，方便软件的安装、更新及移除。所有源自Debian的Linux发行版都使用dpkg，例如Ubuntu、Knoppix 等。
以下是一些 Dpkg 的普通用法：
##### 1、dpkg -i <package.deb>
安装一个 Debian 软件包，如你手动下载的文件，（其中-i等价于--install）
##### 12、dpkg -c <package.deb>
列出<package.deb> 的内容中包含的文件结构（其中-c等价于--contents）
##### 13、dpkg - I<package.deb>
从<package.deb> 中提取包裹信息的详细信息，包括软件名称、版本以及大小等（其中-I等价于--info）
##### 14、dpkg -r <package>
移除一个已安装的包裹（软件名称可通过dpkg -I命令查看，其中-r等价于--remove）
##### 15、dpkg -P <package>
完全清除一个已安装的包裹。和 remove 不同的是，remove 只是删掉数据和可执行文件，purge 另外还删除所有的配制文件。
##### 16、dpkg -L <package>
列出 <package> 安装的软件包安装的所有文件（软件名称可通过dpkg -I命令查看，其中-L等价于--listfiles）
##### 17、dpkg -l <package>
查看<package>软件包的信息（软件名称可通过dpkg -I命令查看，其中-l等价于--list）
##### 18、dpkg -s <package>
显示已安装包裹的详细信息。同时请看 apt-cache 显示 Debian 存档中的包裹信息，以及 dpkg -I 来显示从一个 .deb 文件中提取的包裹信息。（软件名称可通过dpkg -I命令查看，其中-s等价于--status）
##### 19、dpkg-reconfigure <package>
重新配制一个已经安装的包裹，如果它使用的是 debconf (debconf 为包裹安装提供了一个统一的配制界面)。
 
注：dpkg命令无法自动解决依赖关系。如果安装的deb包存在依赖包，则应避免使用此命令，或者按照依赖关系顺序安装依赖包。
 
#### 二、rpm 
rpm 是 redhat 、fedora、suse 的格式。全称为Redhat PackageManager ，是由Redhat 公司提出的，用于管理Linux下软件包的软件。Linux 安装时，除了几个核心模块以外，其余几乎所有的模块均通过RPM 完成安装。
##### 11、rpm -i <package.rpm>
安装需要的包文件，-iv 在安装过程中显示正在安装的文件信息，-ivh 在安装过程中显示正在安装的文件信息及安装进度。
rpm -i example.rpm 安装 example.rpm 包；
rpm -iv example.rpm 安装 example.rpm 包并在安装过程中显示正在安装的文件信息；
rpm -ivh example.rpm 安装 example.rpm 包并在安装过程中显示正在安装的文件信息及安装进度；
 
##### 12、rpm -q …
附加查询命令：
a 查询所有已经安装的包以下两个附加命令用于查询安装包的信息；
i 显示安装包的信息；
l 显示安装包中的所有文件被安装到哪些目录下；
s 显示安装版中的所有文件状态及被安装到哪些目录下；以下两个附加命令用于指定需要查询的是安装包还是已安装后的文件；
p 查询的是安装包的信息；
f 查询的是已安装的某文件信息；
举例如下：
rpm -qa | grep tomcat4 查看 tomcat4 是否被安装；
rpm -qip example.rpm 查看 example.rpm 安装包的信息；
rpm -qif /bin/df 查看/bin/df 文件所在安装包的信息；
rpm -qlf /bin/df 查看/bin/df 文件所在安装包中的各个文件分别被安装到哪个目录下；
 
##### 13、rpm -e 需要卸载的安装包
在卸载之前，通常需要使用rpm -q …命令查出需要卸载的安装包名称。
举例如下：
rpm -e tomcat4 卸载 tomcat4 软件包
 
##### 14、rpm -U 需要升级的包
举例如下：
rpm -Uvh example.rpm 升级 example.rpm 软件包
RPM 验证操作
命令：
##### 15、rpm -V 需要验证的包
举例如下：
rpm -Vf /etc/tomcat4/tomcat4.conf
输出信息类似如下：
1S.5....T c /etc/tomcat4/tomcat4.conf
其中，S 表示文件大小修改过，T 表示文件日期修改过。更多的验证信息请参考rpm 帮助文件：man rpm
注：RPM 的其他附加命令
--force 强制操作如强制安装删除等；
--requires 显示该包的依赖关系；
--nodeps 忽略依赖关系并继续操作；