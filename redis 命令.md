### 启动服务

```
redis-server /usr/local/etc/redis.conf &

```

### 连接服务

```

redis-cli -h 127.0.0.1 -p 6379

```

### 创建软链

```

ln -s /usr/local/redis/bin/redis-server /usr/bin/redis-server


```