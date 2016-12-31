
CentOS用host、dig、nslookup查询DNS命令
(原文地址：http://www.centoscn.com/CentOS/help/2014/0522/3000.html)

一、安装软件包
dig和nslookup需要安装相关软件包。
Centos：

    # yum install bind-utils

Debian：

    # apt-get update
    # apt-get install dnsutils

另外查询前先要在/etc/resolv.conf设置好dns服务器IP。

二、使用方法
1、host命令
host命令是一个简单的DNS查询工具。
一般格式：
host 域名
host -a 域名
常用选项：
-a：相当于"-v -t any"。
-t type：指定要查询的记录类型。默认查询A、AAAA、MX记录。
-v：详细方式输出。
举例：

    # host www.163.com
www.163.com is an alias for www.163.com.lxdns.com.
www.163.com.lxdns.com is an alias for 163.xdwscache.glb0.lxdns.com.
163.xdwscache.glb0.lxdns.com has address 113.107.76.19

2、dig命令
dig命令是一个功能强大的DNS查询命令。
一般格式：
    
    dig [@global-server] [domain] [q-type] [q-class] {q-opt} {d-opt}
参数说明：
    
    @global-server：默认是以/etc/resolv.conf作为DNS查询的主机，这里可以填入其它DNS主机IP。
    domain：要查询的域名。
    q-type：查询记录的类型，例如a、any、mx、ns、soa、hinfo、axfr、txt等，默认查询a。
    q-class：查询的类别，相当于nslookup中的set class。默认值为in（Internet）。
    q-opt：查询选项，可以有好几种方式，比如：-f file为通过批处理文件解析多个地址；-p port指定另一个端口（缺省的DNS端口为53），等等。
    d-opt：dig特有的选项。使用时要在参数前加上一个“+”号。
    d-opt常用选项：
    +vc：使用TCP协议查询。
    +time=###：设置超时时间。
    +trace：从根域开始跟踪查询结果。
举例：
1）
    # dig www.163.com

    ; <<>> DiG 9.8.4-rpz2+rl005.12-P1 <<>> www.163.com
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 60034
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 0
    
    ;; QUESTION SECTION:
    ;www.163.com.			IN	A
    
    ;; ANSWER SECTION:
    www.163.com.		40	IN	CNAME	www.163.com.lxdns.com.
    www.163.com.lxdns.com.	600	IN	CNAME	163.xdwscache.glb0.lxdns.com.
    163.xdwscache.glb0.lxdns.com. 120 IN	A	113.107.76.19
    
    ;; Query time: 779 msec
    ;; SERVER: 8.8.8.8#53(8.8.8.8)
    ;; WHEN: Fri Jan 31 03:23:36 2014
    ;; MSG SIZE  rcvd: 110

2）
    
    # dig +trace www.163.com

    ; <<>> DiG 9.8.4-rpz2+rl005.12-P1 <<>> +trace www.163.com
    ;; global options: +cmd
    .			8854	IN	NS	f.root-servers.net.
    .			8854	IN	NS	c.root-servers.net.
    .			8854	IN	NS	d.root-servers.net.
    .			8854	IN	NS	k.root-servers.net.
    .			8854	IN	NS	a.root-servers.net.
    .			8854	IN	NS	b.root-servers.net.
    .			8854	IN	NS	i.root-servers.net.
    .			8854	IN	NS	g.root-servers.net.
    .			8854	IN	NS	j.root-servers.net.
    .			8854	IN	NS	m.root-servers.net.
    .			8854	IN	NS	e.root-servers.net.
    .			8854	IN	NS	h.root-servers.net.
    .			8854	IN	NS	l.root-servers.net.
    ;; Received 228 bytes from 8.8.8.8#53(8.8.8.8) in 583 ms
    
    com.			172800	IN	NS	j.gtld-servers.net.
    com.			172800	IN	NS	b.gtld-servers.net.
    com.			172800	IN	NS	k.gtld-servers.net.
    com.			172800	IN	NS	l.gtld-servers.net.
    com.			172800	IN	NS	h.gtld-servers.net.
    com.			172800	IN	NS	f.gtld-servers.net.
    com.			172800	IN	NS	m.gtld-servers.net.
    com.			172800	IN	NS	g.gtld-servers.net.
    com.			172800	IN	NS	d.gtld-servers.net.
    com.			172800	IN	NS	c.gtld-servers.net.
    com.			172800	IN	NS	i.gtld-servers.net.
    com.			172800	IN	NS	a.gtld-servers.net.
    com.			172800	IN	NS	e.gtld-servers.net.
    ;; Received 501 bytes from 192.33.4.12#53(192.33.4.12) in 542 ms
    
    163.com.		172800	IN	NS	ns2.nease.net.
    163.com.		172800	IN	NS	ns3.nease.net.
    163.com.		172800	IN	NS	ns4.nease.net.
    163.com.		172800	IN	NS	ns5.nease.net.
    163.com.		172800	IN	NS	ns6.nease.net.
    163.com.		172800	IN	NS	ns1.nease.net.
    ;; Received 242 bytes from 192.43.172.30#53(192.43.172.30) in 471 ms
    
    www.163.com.		600	IN	CNAME	www.163.com.lxdns.com.
    ;; Received 61 bytes from 61.135.255.140#53(61.135.255.140) in 278 ms

3、nslookup
nslookup命令使用频率比dig要高，可能是因为windows上没有dig命令吧。
一般格式：
    
    nslookup [-option] [name | -] [server]
参数说明：
    
    option：表示一些选项。这些选项可以通过set命令设置修改。
    name：表示查询的域名。
    server：可以指定DNS主机IP。
    set命令说明：
    set all：打印当前的选项值。
    set calss=value：设置查询的类型，一般情况下为Internet。
    set debug：设置调试模式。
    set d2：设置详细调试模式。
    set domin=name：设置默认的域名。
    set search：
    set port=value：设置DNS端口。
    set querytype=value：改变查询的信息的类型。默认的类型为A纪录。
    set type=value：和set querytype一样。
    set recurse：设置查询类型为递归；若为set norecurse，查询类型为跌代；缺省为前者。
    set retry=number：设置重试的次数。
    set timeout=number：设置等待应答的限制时间（单位为秒），超出即为超时，如果还可以重试，就会将长超时值加倍，重新查询。
    set vc：通过tcp方式查询。
    set fail：
具体说明可以查看man手册。
举例：
    
    # nslookup www.163.com 4.2.2.2
    
    Server:		4.2.2.2
    Address:	4.2.2.2#53
    
    Non-authoritative answer:
    www.163.com	canonical name = www.163.com.lxdns.com.
    www.163.com.lxdns.com	canonical name = 163.xdwscache.glb0.lxdns.com.
    Name:	163.xdwscache.glb0.lxdns.com
    Address: 113.107.76.19
     
    参考资料：
    http://linux.chinaunix.net/techdoc/system/2008/08/19/1026154.shtml
    http://blog.csdn.net/a8572785/article/details/8641581
    http://blog.chinaunix.net/uid-20615025-id-29801.html