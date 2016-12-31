
* 安装IPy 模块
    
        wget https://pypi.python.org/packages/source/I/IPy/IPy-0.81.tar.gz --no-check-certificate

        tar -zxvf IPy-0.81.tar.gz

        cd IPy-0.81
        
        python setup.py install
        
* 加载 IPy 模块
        
        from IPy import IP

* IP 地址、网段的基本处理

        IP('10.0.0.0/8').version()  #4 代表 IPv4 类型
        4 
        
        IP('::1').version()  #6 代表 IPv6 类型
        6 
        
* 通过指定的网段输出该网段的 IP 个数及所有 IP 地址清单，代码如下：


        from IPy import IP
        ip = IP('192.168.0.0/16')
        print ip.len() # 输出 192.168.0.0/16 网段的 IP 个数
        for x in ip: # 输出 192.168.0.0/16 网段的所有 IP 清单
        print(x)
        
        
* 下面介绍 IP 类几个常见的方法，包括反向解析名称、IP 类型、IP 转换等。
        
        from IPy import IP
        ip = IP('192.168.1.20')
        
        ip.reverseNames() # 反向解析地址格式
        ['20.1.168.192.in-addr.arpa.']
        
        ip.iptype() #192.168.1.20 为私网类型 'PRIVATE'
        IP('8.8.8.8').iptype() #8.8.8.8 为公网类型
        'PUBLIC'
        
        IP("8.8.8.8").int() # 转换成整型格式
        134744072
        
        IP('8.8.8.8').strHex() # 转换成十六进制格式
        '0x8080808'
        
        IP('8.8.8.8').strBin() # 转换成二进制格式
        '00001000000010000000100000001000'
        
        print(IP(0x8080808)) # 十六进制转成 IP 格式
        8.8.8.8        

* IP 方法也支持网络地址的转换，例如根据 IP 与掩码生产网段格式，如下：

        from IPy import IP
        print(IP('192.168.1.0').make_net('255.255.255.0'))
        192.168.1.0/24
        
        print(IP('192.168.1.0/255.255.255.0', make_net=True))
        192.168.1.0/24
        
        print(IP('192.168.1.0-192.168.1.255', make_net=True))
        192.168.1.0/24
        
* 通过 strNormal 方法指定不同 wantprefixlen 参数值以定制不同输出类型的网段。
输出类型为字符串，如下：

        IP('192.168.1.0/24').strNormal(0)
        '192.168.1.0'
        
        IP('192.168.1.0/24').strNormal(1)
        '192.168.1.0/24'
        
        IP('192.168.1.0/24').strNormal(2)
        '192.168.1.0/255.255.255.0'
        
        IP('192.168.1.0/24').strNormal(3)
        '192.168.1.0-192.168.1.255'

* wantprefixlen 的取值及含义：

    * wantprefixlen = 0，无返回，如 192.168.1.0；
    * wantprefixlen = 1，prefix 格式，如 192.168.1.0/24；
    * wantprefixlen = 2，decimalnetmask 格式，如 192.168.1.0/255.255.255.0；
    * wantprefixlen = 3，lastIP 格式，如 192.168.1.0-192.168.1.255。