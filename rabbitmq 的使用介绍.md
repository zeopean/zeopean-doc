### mac 安装rabbitmq

```
# 下载包文件
http://download.csdn.net/detail/tonylllz/9368103

＃ 解压 rabbitmq
tar -zxvf rabbitmq_server-3.5.7.tar.gz

# 启动rabbitmq
cd rabbitmq_server-3.5.7/sbin

./rabbitmq-server restart

# 建立软连接至 /usr/local/bin

ln -s /Users/zeopean/dev-modules/rabbitmq_server-3.5.7/sbin/rabbitmq-plugins  /usr/local/bin/rabbitmq-plugins

ln -s /Users/zeopean/dev-modules/rabbitmq_server-3.5.7/sbin/rabbitmqctl /usr/local/bin/rabbitmqctl

ln -s /Users/zeopean/dev-modules/rabbitmq_server-3.5.7/sbin/rabbitmq-server /usr/local/bin/rabbitmq-server

ln -s /Users/zeopean/dev-modules/rabbitmq_server-3.5.7/sbin/rabbitmq-env /usr/local/bin/rabbitmq-env

 ln -s /Users/zeopean/dev-modules/rabbitmq_server-3.5.7/sbin/rabbitmq-defaults  /usr/local/bin/rabbitmq-defaults

```


### rabbitmq 的使用

```
#开启服务
rabbitmq-server restart

#添加用户
rabbitmqctl add_user daming 123456

#设置管理员账号
rabbitmqctl set_admin daming

#删除用户
rabbitmqctl delete_user guest

#权限设置
rabbitmqctl set_permissions -p "/" daming ".*" ".*" ".*"

#添加虚拟主机
rabbitmqctl add_vhost rabbitmq.demo.host 

#查看rabbitmq 状态
rabbitmqctl status

#查看vhost 状态
rabbitmqctl list_vhosts



```