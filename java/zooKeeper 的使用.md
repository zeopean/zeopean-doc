# 下载 zooKeeper 

```
http://mirrors.hust.edu.cn/apache/kafka/1.0.0/kafka_2.11-1.0.0.tgz

```


# 配置 zooKeeper

```

1. 解压zookeper 包

	tar -zxf zookeeper-3.5.2-alpha.tar.gz 

2. 创建 data 目录
	mv zookeeper-3.5.2-alpha ~/IdeaProjects/zookeeper
	mkdir data
	cd ../conf
	cp zoo_sample.cfg zoo.cfg
	


3. 进行配置 zoo.cfg

	tickTime = 2000
	dataDir = /Users/zeopean/IdeaProjects/zookeeper/data
	clientPort = 2181
	initLimit = 5
	syncLimit = 2




```

# 启动 zooKeeper server 服务

```

cd zookeeper/bin

sh zkServer.sh start | stop 


```

# 启动 zooKeeper cli

```

cd zookeeper/bin

sh zkCli.sh [进入命令窗口] 


```

# 创建节点

```
1. 创建持久节点
	
	create /firstNode "node001"
 
2. 创建顺序节点

	create -s /firstNode "node002"

3. 创建临时节点
 
	create -e /firstNode "node003"

```



# 设置数据

```

set /fitstNode  value001


```




# 获取数据

```

get /fitstNode

get -w /firstNode0000000001


```

# 查看数据


```

ls /firstNode

```


# 状态检查

```

 stat /firstNode

```

# 移除节点

```

rmr /firstNode

```



