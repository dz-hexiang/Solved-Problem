---
title: mosquitto 和 opensips 安装及相关配置
date: 2017-11-21 17:36:17
tags:
---

```
#!/bin/sh
#print hello world in the console window
echo -e "开始安装-----------------------------------------------------------"
echo -e "author:hexiang"
echo -e "name:dz.hexiang"
echo -e "mail:472482006@qq.com"
echo -e "初始设置请稍等..."
sleep 3s

echo -e "开始安装wget下载工具"

yum -y install wget 
echo -e "开始mysql..."
echo -e "下载mysql..."
wget http://repo.mysql.com/mysql-community-release-el7.rpm 
echo -e "解压mysql..."
sudo rpm -ivh mysql-community-release-el7.rpm 
echo -e "解压成功安装mysql..."
yum install mysql-server -y
yum install  mysql-libs mysql-devel -y
echo -e "安装成功，启动mysql..."
systemctl restart  mysqld.service



echo -e "下载语音通话服务器源码..."
cd /home;wget http://opensips.org/pub/opensips/2.2.2/opensips-2.2.2.tar.gz
echo -e "解压语音通话服务器源码..."
tar zxvf  opensips-2.2.2.tar.gz;cd opensips-2.2.2
echo -e "安装语音通话需要的相关环境..."
yum install gcc make -y
yum install flex bison ncurses libncurses-dev ncurses-devel -y
echo -e "开始进入图像配置界面请配只db_mysql..."
make menuconfig;


#提示“请输入姓名”并等待30秒，把用户的输入保存入变量name中
read  -p "请输入ip地址，公网或者局域网IP地址:" myip

sed -i -E "s/^listen=udp:.*$/listen=udp:"$myip":5060/g" /usr/local/etc/opensips/opensips.cfg
echo -e "opensips ip 配置为："$myip
cat /usr/local/etc/opensips/opensips.cfg |grep "listen"


cd /usr/local/sbin/;opensipsdbctl create;
opensipsctl start 
#显示当前在线用户
echo -e "-----------------------------------------------------------"
echo -e "开始即时通信环境..."
yum install gcc-c++ -y
yum install cmake -y
#mosquitto默认支持openssl
yum install openssl-devel -y

echo -e "开始下载即时通信服务器源码..."
cd  /home
wget http://mosquitto.org/files/source/mosquitto-1.4.9.tar.gz
echo -e "开始解压即时通信服务器源码..."
tar -xzvf mosquitto-1.4.9.tar.gz
cd mosquitto-1.4.9;

echo -e "开始进行配置..."

#WITH_SRV ,WITH_UUID,WITH_WEBSOCKETS
sed -i -E "s/^#WITH_SRV:=.*$/WITH_SRV:=yes/g" config.mk
sed -i -E "s/^WITH_SRV:=.*$/WITH_SRV:=yes/g" config.mk

sed -i -E "s/^#WITH_UUID:=.*$/WITH_UUID:=yes/g" config.mk
sed -i -E "s/^WITH_UUID:=.*$/WITH_UUID:=yes/g" config.mk

sed -i -E "s/^#WITH_WEBSOCKETS:=.*$/WITH_WEBSOCKETS:=yes/g" config.mk
sed -i -E "s/^WITH_WEBSOCKETS:=.*$/WITH_WEBSOCKETS:=yes/g" config.mk

echo -e "即时通信配置成功开始安装相关支持库..."
cd /home
wget http://c-ares.haxx.se/download/c-ares-1.10.0.tar.gz
tar xvf c-ares-1.10.0.tar.gz
cd c-ares-1.10.0
./configure
make&make install


yum install libuuid-devel -y

cd /home;
wget https://github.com/warmcat/libwebsockets/archive/v1.3-chrome37-firefox30.tar.gz
tar zxvf v1.3-chrome37-firefox30.tar.gz
cd libwebsockets-1.3-chrome37-firefox30;
mkdir build; cd build;
cmake .. -DLIB_SUFFIX=64
make install

echo -e "即时通信开始编译安装..."
cd /home/mosquitto-1.4.9
make&make install

mv /etc/mosquitto/mosquitto.conf.example /etc/mosquitto/mosquitto.conf


echo -e "配置相关信息..."
sed -i -E "s/^#autosave_interval 1800$/autosave_interval 1800/g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^#persistence false$/persistence true/g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^#persistence_file mosquitto.db$/persistence_file mosquitto.db/g" /etc/mosquitto/mosquitto.conf

sed -i -E "s/^autosave_interval 1800$/#autosave_interval 1800/g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^persistence true$/#persistence true/g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^persistence_file mosquitto.db$/#persistence_file mosquitto.db/g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^persistence_location \/var\/mosquitto\/$/#persistence_location \/var\/mosquitto\//g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^listener 1883$/#listener 1883/g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^listener 8888$/#listener 8888/g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^protocol websockets$/#protocol websockets/g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^user root$/#user root/g" /etc/mosquitto/mosquitto.conf
sed -i -E "s/^allow_anonymous true$/#allow_anonymous true/g" /etc/mosquitto/mosquitto.conf

sed -i -E '$ a autosave_interval 1800' /etc/mosquitto/mosquitto.conf
sed -i -E "$ a persistence true" /etc/mosquitto/mosquitto.conf
sed -i -E '$ a persistence_file mosquitto.db' /etc/mosquitto/mosquitto.conf
sed -i -E '$ a persistence_location /var/mosquitto/' /etc/mosquitto/mosquitto.conf
sed -i -E '$ a listener 1883' /etc/mosquitto/mosquitto.conf
sed -i -E '$ a listener 8888' /etc/mosquitto/mosquitto.conf
sed -i -E '$ a protocol websockets' /etc/mosquitto/mosquitto.conf
sed -i -E '$ a user root' /etc/mosquitto/mosquitto.conf
sed -i -E '$ a allow_anonymous true' /etc/mosquitto/mosquitto.conf

#sed -i -E '$ a --------------' /etc/mosquitto/mosquitto.conf

touch /etc/ld.so.conf.d/liblocal.conf
#添加下面两行配置

echo -e '/usr/local/lib64\n/usr/local/lib'>/etc/ld.so.conf.d/liblocal.conf

#刷新
ldconfig

echo -e "启动即时通信服务..."
cd /usr/local/sbin
mosquitto -c /etc/mosquitto/mosquitto.conf -d


echo -e "-----------------------------------------------------------"
echo -e "配置防火墙..."


#安装iptables-services
yum install iptables-services -y
#启动firewalld服务
echo -e "设置开机启动防火墙..."
systemctl enable firewalld.service
echo -e "启动防火墙..."
systemctl start firewalld.service
echo -e "设置开机启动防火墙规则..."
systemctl enable iptables.service
echo -e "启动防火墙规则..."
systemctl start iptables.service
#查看iptables现有规则
iptables -L -n
#先允许所有,不然有可能会杯具
iptables -P INPUT ACCEPT
#清空所有默认规则
iptables -F
#清空所有自定义规则
iptables -X

#所有计数器归0
iptables -Z
echo -e "开启各种服务端口..."
#开放1888 端口
iptables -A INPUT -p tcp --dport 1888 -j ACCEPT
#开放8888端口
iptables -A INPUT -p tcp --dport 1883 -j ACCEPT

iptables -A INPUT -p tcp --dport 8888 -j ACCEPT
#开放8888端口

iptables -A INPUT -p udp --dport 5060 -j ACCEPT

#开放8888端口
iptables -A INPUT -p tcp --dport 8087 -j ACCEPT
iptables -A INPUT -p tcp --dport 8088 -j ACCEPT
iptables -A INPUT -p tcp --dport 8086 -j ACCEPT
iptables -A INPUT -p tcp --dport 8085 -j ACCEPT
iptables -A INPUT -p tcp --dport 1935 -j ACCEPT
#保存上述规则
service iptables save


#查看状态
systemctl restart iptables.service




echo -e "下面设置开机自动启动各种服务..."



#echo -e 'mosquitto -c /etc/mosquitto/mosquitto.conf -d\ncd /usr/local/sbin/ ; ./opensipsctl start\nsystemctl restart WowzaStreamingEngine.service\nsystemctl restart  iptables.service'>/etc/rc.d/rc.local

#2.加入以下命令


chmod +x /etc/rc.d/rc.local 
sed -i -E '$ a mosquitto -c \/etc\/mosquitto\/mosquitto.conf -d' /etc/rc.d/rc.local
sed -i -E '$ a cd \/usr\/local\/sbin\/ ; .\/opensipsctl start' /etc/rc.d/rc.local
sed -i -E '$ a systemctl restart  iptables.service' /etc/rc.d/rc.local
sed -i -E '$ a systemctl restart WowzaStreamingEngine.service' /etc/rc.d/rc.local
```

