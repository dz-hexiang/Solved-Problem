---
title: ubuntu没有messages日志
date: 2017-4-15 17:36:17
tags:
---
#### 没有/var/log/messages

```
vim /etc/rsyslog.d/50-default.conf
```

#### 打开文件 将 /var/log/messages项目的解注释掉并重启生效