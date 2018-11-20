## emqx 的简单使用

```

# 启动emqx
./bin/emqx start

# 检查运行状态
./bin/emqx_ctl status

# 停止emqx
./bin/emqx stop

```


## 重要端口

```

1883	MQTT 协议端口
8883	MQTT/SSL 端口
8083	MQTT/WebSocket 端口
8084	MQTT/WebSocket/SSL 端口


```

## 相关配置文件

```

配置文件					说明
etc/emqx.conf				EMQ X R3.0 消息服务器配置文件
etc/acl.conf				EMQ X R3.0 默认ACL规则配置文件
etc/plugins/*.conf		EMQ X R3.0 各类插件配置文件



```

## 环境变量

```

EMQX_NODE_NAME			Erlang 节点名称，例如: emqx@127.0.0.1
EMQX_NODE_COOKIE			Erlang 分布式节点通信 Cookie
EMQX_MAX_PORTS			Erlang 虚拟机最大允许打开文件 Socket 数
EMQX_TCP_PORT	MQTT/TCP 	监听端口，默认: 1883
EMQX_SSL_PORT	MQTT/SSL 	监听端口，默认: 8883
EMQX_WS_PORT				MQTT/WebSocket 监听端口，默认: 8083
EMQX_WSS_PORT				MQTT/WebSocket/SSL 监听端口，默认: 8084



```


## 进程数 限制


```

node.process_limit	Erlang 虚拟机允许的最大进程数，EMQ 一个连接会消耗2个Erlang进程
node.max_ports	Erlang 虚拟机允许的最大 Port 数量，EMQ 一个连接消耗1个 Port

- 警告
实际连接数量超过 Erlang 虚拟机参数设置，会引起 EMQ 消息服务器宕机!

```


### 服务监听

 listener 段落设置最大允许连接数:
 
```

listener.tcp.external = 0.0.0.0:1883
listener.tcp.external.acceptors = 8
listener.tcp.external.max_clients = 1024
 
 ```
 
## MQTT 协议参数配置

### MQTT 最大报文尺寸

```
## Max Packet Size Allowed, 1MB by default
mqtt.max_packet_size = 1MB

```

### ClientId 最大允许长度
```
## Max ClientId Length Allowed
mqtt.max_clientid_len = 65535
```

### Topic 最大允许等级
```
## Max Topic Levels Allowed
mqtt.max_topic_levels = 0
```

### Qos 最大允许值
```
## Maximum QoS allowed
mqtt.max_qos_allowed = 2
```

### Topic Alias 最大数量
```
## Maximum Topic Alias, 0 means no limit
mqtt.max_topic_alias = 0
```

### 启用MQTT Retain Messages

```
## Enable MQTT Retain Messages
mqtt.retain_available = true
```

### 启用MQTT Wildcard Subscriptions

```
## Enable MQTT Wildcard Subscriptions
mqtt.wildcard_subscription = true
```

## 启用MQTT Shared Subscriptions
```
## Enable MQTT Shared Subscriptions
mqtt.shared_subscription = true
```

### 消息队列类型
```
## Message queue type, Enum: simple, priority
mqtt.mqueue_type = simple
```

###定义主题优先度

```
## Topic priorities, Default is 0
## mqtt.mqueue_priorities = topic/1=10,topic/2=8
```
