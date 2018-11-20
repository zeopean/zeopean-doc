## zookeeper 的使用

### 开启/关闭/重启 服务

```

./zkServer.sh start local

./zkServer.sh stop

./zkServer.sh restart

```

### 查看服务状态

```
./zkServer.sh stats

```


### 连接服务

```
./zkCli.sh -server localhost:2181


```

### 增删改查 操作

```

create /node helloWord

get /node

set /node hellword-zeopean

delete /node

stat /node

```

### setquota -n|-b val path：限制节点的值的长度或其子节点的个数

-n 限制节点(包含当前节点)的个数为val
-b 限制节点值的长度为val
path 要限制的节点路径


### listquota path：查看节点配额情况

### delquota [-n|-b] path：删除配额信息

### rmr path：循环删除路径下的节点


### history：列出已操作的指令记录

### redo cmdno：重新执行history中的命令

### quit：退出zookeeper客户端连接

### close：关闭connect连接的服务器

