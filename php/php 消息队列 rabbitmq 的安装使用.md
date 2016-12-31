
今天尝试安装了 rabbitmq ，用作php 的消息队列，下面是具体的步骤

* 首先呢，需要安装 rabbitmq 服务
        
        # 进行yum 安装
        yum -y install erlang rabbitmq-server
        # 开启服务
        service rabbitmq-server start
        # 开启启动
        chkconfig rabbitmq-server on

* 接着呢，需要在github 下载这个包，我这里用的是 v0.5.2 版本的
    
    [rabbitmq v0.5.2](https://github.com/alanxz/rabbitmq-c/archive/master.zip)

* 接下来，通过 使用 .sh脚本，进行安装
        
        #切换目录到 rabbittmq-c ，更改文件属性
            chmod -a+x travis.sh

        #初始化
            ./travis.sh  autotools    

        #安装    
            ./travis.sh  cmake


* 再然后，使用  pecl 安装php 的 amqp 模块
    
        pecl install amqp
        #使用 pecl 可以不用在平php.ini 文件中添加 amqp.so

* 最后，查看phpinfo ，可以看到安装成功
    
        amqp

        Version	        1.7.0
        Revision	    release
        Compiled	    May 2 2016 @ 01:44:24
        AMQP protocol  version	0-9-1
        librabbitmq version	    0.8.1-pre
        Default max channels per connection	256
        Default max frame size	131072
        Default heartbeats interval	0