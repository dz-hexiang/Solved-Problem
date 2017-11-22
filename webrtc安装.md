---
title: webrtc安装
date: 2017-11-21 17:36:17
tags:
---
#### 1.下载python 并安装

```
wget https://www.python.org/ftp/python/2.7.13/Python-2.7.13.tgz
tar zxvf Python-2.7.13.tgz
cd Python-2.7.13
./configure
make&make instal
```

l




#### 2.安装Nodejs

#### 安装git

```
apt-get install git
```

#### 安装nodejs

```
sudo apt-get install -y nodejs
```

#### 当安装好nodejs后 node 命令依然无效时候执行

```
sudo apt-get install -y nodejs-legacy
```

#### nodejs 软件管理工具

```
sudo apt-get install -y npm
```

#### 测试 是否安装好 查看版本

```
node --version
```


#### 3.安装Grunt

```
npm install grunt
```

#### 4. 翻墙

```
wget https://raw.githubusercontent.com/getlantern/lantern-binaries/master/lantern-installer-64-bit.deb
su root
dpkg -i lantern-installer-64-bit.deb
```


#### 5. Google App Engine SDK for Python 安装

```
wget https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-163.0.0-linux-x86_64.tar.gz
tar zxvf google-cloud-sdk-163.0.0-linux-x86_64.tar.gz
./google-cloud-sdk/install.sh
./google-cloud-sdk/bin/gcloud init
```



#### sudo apt-get install golang


```
rm -rf collider collidermain collidertest golang.org

 
export GOROOT=/usr/share/go-1.6/
export GOPATH=/usr/share/go-1.6/
 
export APPRTC=/home/hexiang/Downloads/apprtc/
ln -s $APPRTC/src/collider/collider $GOPATH/src/
ln -s $APPRTC/src/collider/collidermain $GOPATH/src/
ln -s $APPRTC/src/collider/collidertest $GOPATH/src/

go get collidermain
```

#### 如提示：cannot find package "golang.org/x/net/websocket"翻墙后

```
go get -v golang.org/x/net/websocket golang.org/x/net/websocket
```

