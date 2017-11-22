---
title: 查看linux版本
date: 2017-10-21 17:36:17
tags:
---
#### 1.查看系统版本

```
cat /etc/redhat-release 

cat /etc/issue 
```

#### 2.查看内核版本

```
cat /proc/version 

uname -a 
```

#### 3.查看64位还是32位： 

```
getconf LONG_BIT 

file /bin/ls 
```

