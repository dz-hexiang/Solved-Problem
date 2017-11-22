---
title: linux没有网络
date: 2017-11-21 17:36:17
tags:
---
#### 1.打开文件

```
vim /etc/rc.d/rc.local
```

#### 2.加入以下命令

```
mosquitto -c /etc/mosquitto/mosquitto.conf -d
cd /usr/local/sbin/ ; ./opensipsctl start
systemctl restart WowzaStreamingEngine.service
systemctl restart  iptables.service
```


#### 3.添加执行权限

```
chmod +x /etc/rc.d/rc.local
```

 


#### 4.重启后生效，开机后将自动启动即时通信、语音对讲、流媒体、防火墙规则服务等

