#查看8088端口是否被占用
netstat -aon|findstr "8088"  

#查看8088端口是被什么进程占用
tasklist|findstr "2724"

#结束进程
taskkill /pid "5432"