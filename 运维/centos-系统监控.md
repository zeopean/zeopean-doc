系统监控
#### 查看系统信息

```
- 资源
# uname -a                  # 查看内核/操作系统/CPU信息
# head -n 1 /etc/issue      # 查看操作系统版本
# hostname                  # 查看计算机名
# cat /proc/cpuinfo         # 查看CPU信息
# lsmod                     # 列出加载的内核模块
# env                       # 查看环境变量
# free -m                   # 查看内存使用量和交换区使用量
# grep MemTotal /proc/meminfo       # 查看内存总量
# grep MemFree /proc/meminfo        # 查看空闲内存量
# uptime                    # 查看系统运行时间、用户数、负载
# cat /proc/loadavg         # 查看系统负载
# ps -ef                    # 查看所有进程
# top                       # 实时显示进程状态

- 网络
# ifconfig                  # 查看所有网络接口的属性
# iptables -L               # 查看防火墙设置
# route -n                  # 查看路由表
# netstat -lntp             # 查看所有监听端口
# netstat -antp             # 查看所有已经建立的连接
# netstat -s                # 查看网络统计信息

- 用户
# w                         # 查看活动用户
# id < 用户名>              # 查看指定用户信息
# last                      # 查看用户登录日志
# cut /etc/passwd           # 查看系统所有用户
# cut /etc/group            # 查看系统所有组
# crontab -l                # 查看所有用户的定时任务

- 磁盘
# df -h                     # 查看各分区使用情况
# du -sh < 目录名>          # 查看指定目录的大小
# mount | column -t         # 查看挂接的分区状态
# fdisk -l                  # 查看所有分区
# swapon -s                 # 查看所有交换分区
# hdparm -i /dev/hda        # 查看磁盘参数(仅适用于IDE设备)
# dmesg | grep IDE          # 查看启动时IDE设备检测状况

```



#### vmstat 的使用
```
    vmstat 2 1     #2表示每个两秒采集一次服务器状态，1表示只采集一次。
```
**参数解析**
```
r 表示运行队列(就是说多少个进程真的分配到CPU)，我测试的服务器目前CPU比较空闲，没什么程序在跑，当这个值超过了CPU数目，就会出现CPU瓶颈了。这个也和top的负载有关系，一般负载超过了3就比较高，超过了5就高，超过了10就不正常了，服务器的状态很危险。top的负载类似每秒的运行队列。如果运行队列过大，表示你的CPU很繁忙，一般会造成CPU使用率很高。

b 表示阻塞的进程,这个不多说，进程阻塞，大家懂的。

swpd 虚拟内存已使用的大小，如果大于0，表示你的机器物理内存不足了，如果不是程序内存泄露的原因，那么你该升级内存了或者把耗内存的任务迁移到其他机器。

free   空闲的物理内存的大小，我的机器内存总共8G，剩余3415M。

buff   Linux/Unix系统是用来存储，目录里面有什么内容，权限等的缓存，我本机大概占用300多M

cache cache直接用来记忆我们打开的文件,给文件做缓冲，我本机大概占用300多M(这里是Linux/Unix的聪明之处，把空闲的物理内存的一部分拿来做文件和目录的缓存，是为了提高 程序执行的性能，当程序使用内存时，buffer/cached会很快地被使用。)

si  每秒从磁盘读入虚拟内存的大小，如果这个值大于0，表示物理内存不够用或者内存泄露了，要查找耗内存进程解决掉。我的机器内存充裕，一切正常。

so  每秒虚拟内存写入磁盘的大小，如果这个值大于0，同上。

bi  块设备每秒接收的块数量，这里的块设备是指系统上所有的磁盘和其他块设备，默认块大小是1024byte，我本机上没什么IO操作，所以一直是0，但是我曾在处理拷贝大量数据(2-3T)的机器上看过可以达到140000/s，磁盘写入速度差不多140M每秒

bo 块设备每秒发送的块数量，例如我们读取文件，bo就要大于0。bi和bo一般都要接近0，不然就是IO过于频繁，需要调整。

in 每秒CPU的中断次数，包括时间中断

cs 每秒上下文切换次数，例如我们调用系统函数，就要进行上下文切换，线程的切换，也要进程上下文切换，这个值要越小越好，太大了，要考虑调低线程或者进程的数目,例如在apache和nginx这种web服务器中，我们一般做性能测试时会进行几千并发甚至几万并发的测试，选择web服务器的进程可以由进程或者线程的峰值一直下调，压测，直到cs到一个比较小的值，这个进程和线程数就是比较合适的值了。系统调用也是，每次调用系统函数，我们的代码就会进入内核空间，导致上下文切换，这个是很耗资源，也要尽量避免频繁调用系统函数。上下文切换次数过多表示你的CPU大部分浪费在上下文切换，导致CPU干正经事的时间少了，CPU没有充分利用，是不可取的。

us 用户CPU时间，我曾经在一个做加密解密很频繁的服务器上，可以看到us接近100,r运行队列达到80(机器在做压力测试，性能表现不佳)。

sy 系统CPU时间，如果太高，表示系统调用时间长，例如是IO操作频繁。

id  空闲 CPU时间，一般来说，id + us + sy = 100,一般我认为id是空闲CPU使用率，us是用户CPU使用率，sy是系统CPU使用率。

wt 等待IO CPU时间。


```



**apache 监控**

（借鉴：http://wpguru.co.uk/2012/06/how-to-install-apachetop-on-centos/）

安装
    
    yum install apachetop
    
    # 查看apache情况
    apachetop
    
    
**mysql 监控**

（文章：http://www.cyberciti.biz/tips/how-do-i-monitor-what-my-mysql-server-is-doing.html） 

    yum install mytop
    
* yum镜像暂时下不到
* 晚点完善



**iotop**

是一个用来监视磁盘 I/O 使用状况的 top 类工具。如下图所示，Iotop 具有与 top 相似的 UI，其中包括 PID、用户、I/O、进程等相关信息。
    
* 安装
        
        ubuntu:apt-get install iotop
        centos:yum install iotop

    
* 使用方法
    
        iotop [OPTIONS]
        主要选项有：
        -o :只显示有io操作的进程
        -b :批量显示，无交互。主要用作记录到文件。
        -n NUM:显示NUM次，主要用于非交互式模式。
        -d SEC：间隔SEC秒显示一次。
        -p PID:监控的进程pid
        -u USER:监控的进程用户。

**nmap**
    (文章参考：http://blog.jobbole.com/54595/)
    
* 安装
    
        yum install nmap    

* 使用
        
        #域名
        nmap [-v] www.zeopean.com
        
        # ip 地址
        nmap  192.168.11.20 
    
        #多个ip
        nmap 192.168.0.101,102,103

        nmap  192.168.11.20 192.168.11.. ...

        #整个子网
        name 192.168.11.*


* 这篇文章很有用
    
    http://www.yunweipai.com/archives/6213.html
    
    
    

