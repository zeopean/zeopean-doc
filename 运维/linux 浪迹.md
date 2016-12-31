- linux 间的文件传输
		
		scp -r ./mysql-5.5.28.tar.gz root@192.168.31.100:/home/zeopean




- centos 7 网络知识
	
	-- 查看ip信息
	$ ip add
	
	-- 查看路由列表
	$ ip route list
	$ ip route show

	-- ss -ant 代替  netstat 


- 配置centos 网络

	-- dhcp
			修改 /etc/sysconfig/network-sctipts/ifcfg-enp0s3 文件，把 ONBOOT 设置为 yes
	
	


- 修改mysql root 密码
```	

	1.0
	SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpass');

	1.1
	用UPDATE直接编辑user表

	　　mysql -u root
	
	　　mysql> use mysql;
	
	　　mysql> UPDATE user SET Password = PASSWORD('newpass') WHERE user = 'root';
	
	　　mysql> FLUSH PRIVILEGES;
	
	1.2
	在丢失root密码的时候，可以这样
	
	　　mysqld_safe --skip-grant-tables&
	
	　　mysql -u root mysql
	
	　　mysql> UPDATE user SET password=PASSWORD("new password") WHERE user='root';
	
	　　mysql> FLUSH PRIVILEGES;

	
```




-  查看系统编码

		 echo $LANG


- 查看进程pid
		 
		 ps -ef | grep nginx


- 查找大文件夹

	du -h --max-depth=2 | sort -nr | head -12


- 解析 /var/log 文件
```

	系统的引导日志:/var/log/boot.log
	例如:Feb 26 10:40:48 sendmial : sendmail startup succeeded
	就是邮件服务启动成功!
	
	系统日志一般都存在/var/log下
	常用的系统日志如下:
	核心启动日志:/var/log/dmesg
	系统报错日志:/var/log/messages
	邮件系统日志:/var/log/maillog
	FTP系统日志:/var/log/xferlog
	安全信息和系统登录与网络连接的信息:/var/log/secure
	登录记录:/var/log/wtmp      记录登录者讯录，二进制文件，须用last来读取内容    who -u /var/log/wtmp 查看信息
	News日志:/var/log/spooler
	RPM软件包:/var/log/rpmpkgs
	XFree86日志:/var/log/XFree86.0.log
	引导日志:/var/log/boot.log   记录开机启动讯息，dmesg | more
	cron(定制任务日志)日志:/var/log/cron
	 
	安全信息和系统登录与网络连接的信息:/var/log/secure
	 
	文件 /var/run/utmp 記錄著現在登入的用戶。
	文件 /var/log/wtmp 記錄所有的登入和登出。
	文件 /var/log/lastlog 記錄每個用戶最後的登入信息。
	文件 /var/log/btmp 記錄錯誤的登入嘗試。
	 
	less /var/log/auth.log 需要身份确认的操作

```



- 2016-3-17 查看linux 登录信息

```	
    查看登录成功的用户信息
	命令: last
	最新的登录记录在最前面，所以可以用 一下命令来查看。
		
		last | less
	
	查看登录失败的用户信息
	命令: lastb
	
	查看登录日志
	命令:  tail /var/log/secure

```

- 查看端口号
	
	netstat -aon|findstr "80" 
	
- 列出所有进程
	
    tasklist



- 2016-1-8 tcpdump 的使用

	- tcpdump 抓包解析 
	
	- tcpdump -i eth0 -nn -X ‘port 53’ -c 1
```
	-nn选项：
	意思是说当tcpdump遇到协议号或端口号时，不要将这些号码转换成对应的协议名称或端口名称。比如，众所周知21端口是FTP端口，我们希望显示21，而非tcpdump自作聪明的将它显示成FTP。

	-X选项：
	告诉tcpdump命令，需要把协议头和包内容都原原本本的显示出来（tcpdump会以16进制和ASCII的形式显示），这在进行协议分析时是绝对的利器。

	‘port 53’：
	这是告诉tcpdump不要看到啥就显示啥。我们只关心源端口或目的端口是53的数据包，其他的数据包别给我显示出来。

	-c选项：
	是Count的含义，这设置了我们希望tcpdump帮我们抓几个包。我设置的是1，所以tcpdump不会帮我再多抓哪怕一个包回来。
```
	-- 【-e选项】- 增加以太网帧头部信息输出
		# tcpdump -i eth0 -c 1 -e


	-- 【-l选项】- 使得输出变为行缓冲
		# tcpdump -i eth0 -l |awk '{print $1}'

	-- 【-t选项】- 输出时不打印时间戳
		# tcpdump -i eth0 -c 1 -t

	--【-v选项】- 输出更详细的信息
		# tcpdump -i eth0 -c 1 -v

	--【-F选项】- 指定过滤表达式所在的文件
		# tcpdump -i eth0 -c 1 -t -F filter.txt

	-- 【-w选项】- 将流量保存到文件中
		# tcpdump -i eth0 -w flowdata

	-- 【-r选项】- 读取raw packets文件 (# less flowdata)
		# tcpdump -r flowdata 
		


	-- 我只想查目标机器端口是53或80的网络包，其他端口的我不关注
		# tcpdump -i eth0 -c 3 'dst port 53 or dst port 80'


	--【我想专门查看这个源机器和那个目的机器之间的网络包，不想被其他无关的机器打扰】
		# tcpdump -i eth0 'dst 8.8.8.8'

	--【我只想抓UDP的包，不想被TCP的包打扰】
		# tcpdump -i eth0 -c 10 'udp'



- 2016-1-8 awk 的基本使用 
	```
     统计/etc/passwd: 				   
     文件名 				  每行的行号     每行的列数 	    对应的完整行内容
		#awk  -F ':'  '{print "filename:" FILENAME ",linenumber:" NR ",columns:" NF ",linecontent:" $0 }' /etc/passwd
	或者
		awk  -F ':'  '{printf("filename:%10s,linenumber:%s,columns:%s,linecontent:%s\n",FILENAME,NR,NF,$0)}' /etc/passwd
    ```
    
- 2016-1-8 swoole + php client端的使用
	http://wiki.swoole.com/wiki/page/1.html
	-- demo test script  测试
		
		-- server.php:
		<?php
		  $serv = new swoole_server("0.0.0.0", 9501);
		  $serv->on('connect', function ($serv, $fd){
		    echo "Client:Connect.\n";
		  });
		  $serv->on('receive', function ($serv, $fd, $from_id, $data) {
		    $serv->send($fd, 'Swoole: '.$data);
		  });
		  $serv->on('close', function ($serv, $fd) {
		    echo "Client: Close.\n";
		  });
		  $serv->start();
		?>


		-- client.php:
		<?php
		  $client = new swoole_client(SWOOLE_SOCK_TCP, SWOOLE_SOCK_ASYNC);
		  $client->on("connect", function($cli) {
		    $cli->send("hello world\n");
		  });
		  $client->on("receive", function($cli, $data){
		    echo "Receive: $data\n";
		  });
		  $client->on("error", function($cli){
		    echo "connect fail\n";
		  });
		  $client->on("close", function($cli){
		    echo "close\n";
		  });
		  $client->connect('127.0.0.1', 9501, 0.5);
		?>
	-- 1、先执行 php server.php   
	-- 2、再执行 php client.php


- 2016-1-8 检验服务器是否 ok

	curl -I -s www.qq.com  |head -1|awk '{ health = $2=="200"?"server is ok":"server is bad"}END{print health}'

- 2016-1-8 substr_count 获取字符出现次数

	int substr_count ( string $haystack , string $needle [, int $offset = 0 [, int $length ]] )
	substr_count() 返回子字符串needle 在字符串 haystack 中出现的次数。注意 needle 区分大小写。

