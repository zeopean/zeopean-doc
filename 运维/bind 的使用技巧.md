
-- 2016-4-13
配置dns （根据鸟哥的方法 http://linux.vbird.org/linux_server/0350dns.php#server_settings ）：

1. 先安装 bind 
    
        yum install bind bind-utils bind-libs

2. 配置 /etc/named.conf
        
        options {
        	listen-on port 53 { any; };
        	listen-on-v6 port 53 { ::1; };
        	directory 	"/var/named";	
        	dump-file 	"/var/named/data/cache_dump.db";	
        	statistics-file "/var/named/data/named_stats.txt";	
        	memstatistics-file "/var/named/data/named_mem_stats.txt"; 
        	allow-query     { any; };	
        	allow-query-cache { any;};   	
        	
        	allow-transfer { none; };
        
        	recursion yes;   
        
        };

        zone "." IN {
        	type hint;
        	file "named.ca";
        };
        zone "daming.com" IN {
        	type master;
        	file "named.daming.com";
        };
        zone "31.168.192.in-addr.arpa" IN {
        	type master;
        	file "named.192.168.31";
        };

3. 创建，配置 /var/named/named.daming.com
        
        $TTL 600
        @    IN SOA   master.daming.com. admin.daming.com. (
                                         2011080401 3H 15M 1W 1D ) ; 與上面是同一行
        @                       IN NS    master.daming.com.  ; DNS 伺服器名稱
        master.daming.com.      IN A     192.168.31.100         ; DNS 伺服器 IP
        @                       IN MX 10 www.daming.com.     ; 領域名稱的郵件伺服器
        
        www.daming.com.       IN A     192.168.31.100
        linux.daming.com.     IN CNAME www.daming.com.
        ftp.daming.com.       IN CNAME www.daming.com.
        
        slave.daming.com.       IN A    192.168.31.165
        clientlinux.daming.com. IN A    192.168.31.200

4. 创建，配置 /var/named/named.192.168.31
    
        $TTL    600
        @       IN SOA  master.daming.com. admin.daming.com. (
                        2011080401 3H 15M 1W 1D )
        @       IN NS   master.daming.com.
        100     IN PTR  master.daming.com.  ; 將原本的 A 改成 PTR 的標誌而已
        
        100     IN PTR  www.daming.com.     ; 這些是特定的 IP 對應
        165     IN PTR  slave.daming.com.
        20      IN PTR  clientlinux.daming.com

5. 重启 named 服务，查看状态
    
        # systemctl restart named
        # systemctl status named


6. 进行测试
        
        # dig master.daming.com
        # dig www.daming.com



-- 2016-4-11

BIND为我们提供了两个语法检查工具：
named-checkconf可以查看BIND主配置文件的错误：
            
    named-checkconf /var/named/chroot/etc/named.conf

named-checkzone可以查看zone文件的错误：
            
    named-checkzone example.com /var/named/chroot/var/named/example.com.zone 
            
            
通常，BIND配置要么语法上出错、要么权限上有错