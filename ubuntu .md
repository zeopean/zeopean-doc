## 网络相关

```

重启指定网卡
　　ifdown eth0 && ifup eth0


重启除lo网卡的所有网卡
　　ifdown --exclude=lo -a && sudo ifup --exclude=lo -a



```

