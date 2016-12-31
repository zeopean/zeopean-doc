
Google的公共DNS解析服务

    配置的所有个人电脑与服务器都是用8.8.8.8与8.8.4.4做客户端解析。
    

Linux下设置：

打开命令终端，分别运行

    echo nameserver 8.8.8.8 > /etc/resolv.conf
    echo nameserver 8.8.4.4 > /etc/resolv.conf