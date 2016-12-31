**centos65 防火墙**

（学习自:http://vbird.dic.ksu.edu.tw/linux_server/0250simple_firewall_3.php）

防火墙参数

    [root@www ~]# iptables [-t tables] [-L] [-nv]
    选项与参数：
    -t ：后面接 table ，例如 nat 或 filter ，若省略此项目，则使用默认的 filter
    -L ：列出目前的 table 的规则
    -n ：不进行 IP 与 HOSTNAME 的反查，显示讯息的速度会快很多！
    -v ：列出更多的信息，包括通过该规则的封包总位数、相关的网络接口等
    
    范例：**列出 filter table 三条链的规则**
    
    [root@www ~]# iptables -L -n
    
    Chain INPUT (policy ACCEPT)   <==针对 INPUT 链，且预设政策为可接受
    target  prot opt source     destination <==说明栏
    ACCEPT  all  --  0.0.0.0/0  0.0.0.0/0   state RELATED,ESTABLISHED <==第 1 条规则
    ACCEPT  icmp --  0.0.0.0/0  0.0.0.0/0                             <==第 2 条规则
    ACCEPT  all  --  0.0.0.0/0  0.0.0.0/0                             <==第 3 条规则
    ACCEPT  tcp  --  0.0.0.0/0  0.0.0.0/0   state NEW tcp dpt:22      <==以下类推
    REJECT  all  --  0.0.0.0/0  0.0.0.0/0   reject-with icmp-host-prohibited
    
    Chain FORWARD (policy ACCEPT)  <==针对 FORWARD 链，且预设政策为可接受
    target  prot opt source     destination
    REJECT  all  --  0.0.0.0/0  0.0.0.0/0   reject-with icmp-host-prohibited
    
    Chain OUTPUT (policy ACCEPT)  <==针对 OUTPUT 链，且预设政策为可接受
    target  prot opt source     destination
    
    范例：**列出 nat table 三条链的规则**
    
    [root@www ~]# iptables -t nat -L -n
    
    Chain PREROUTING (policy ACCEPT)
    target     prot opt source               destination
    
    Chain POSTROUTING (policy ACCEPT)
    target     prot opt source               destination
    
    Chain OUTPUT (policy ACCEPT)
    target     prot opt source               destination

***参数说明***

    target：代表进行的动作， ACCEPT 是放行，而 REJECT 则是拒绝，此外，尚有 DROP (丢弃) 的项目！
    prot：代表使用的封包协议，主要有 tcp, udp 及 icmp 三种封包格式；
    opt：额外的选项说明
    source ：代表此规则是针对哪个『来源 IP』进行限制？
    destination ：代表此规则是针对哪个『目标 IP』进行限制？


查看防火墙规则
    
    [root@www ~]# iptables-save [-t table]
    #选项与参数：
    -t ：可以仅针对某些表格来输出，例如仅针对 nat 或 filter 等等


清楚防火墙规则
    
    [root@www ~]# iptables [-t tables] [-FXZ]
    # 选项与参数：
    -F ：清除所有的已订定的规则；
    -X ：杀掉所有使用者 "自定义" 的 chain (应该说的是 tables ）啰；
    -Z ：将所有的 chain 的计数与流量统计都归零
    
    # 范例：清除本机防火墙 (filter) 的所有规则
    [root@www ~]# iptables -F
    [root@www ~]# iptables -X
    [root@www ~]# iptables -Z



关闭防火墙
        
        /etc/init.d/iptables stop #需要切换到root用户
        
        
查看防火墙信息
        
        /etc/init.d/iptables status
        

开放8080端口，编辑防火墙配置文件
        
    vi + /etc/sysconfig/iptables
    # 增加以下代码 
    -A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT        
    

重启防火墙

    service iptables restart

永久关闭防火墙
    
    chkconfig –level 35 iptables off