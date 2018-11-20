### 查看 linux 版本

```

lsb_release -a

```



### 查看系统存在的定时任务 

```
crontab -l

```

### 查看内存条数
```

dmidecode | grep -A16 "Memory Device$"

```

### 查看 内存

```
free -m

```

### linux 系统日志管理

- 查看服务是否存在


```
ps -aux | grep syslog 

# 检查syslog 服务
chkconfig --list syslog

auditd         	0:off	1:off	2:on	3:on	4:on	5:on	6:off
h

```

- 检查syslog 服务


```

chkconfig --list syslog

auditd         	0:off	1:off	2:on	3:on	4:on	5:on	6:off



```

- 产看用户日志

```
cat /var/log/secure

```

- 系统的日志配置，见文件

```

/etc/rsyslog.conf

```


