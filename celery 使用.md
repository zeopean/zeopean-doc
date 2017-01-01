Celery 也定义了一组用于安装 Celery 和给定特性依赖的捆绑。

你可以在 requirements.txt 中指定或在 pip 命令中使用方括号。多个捆绑用逗号分隔。

$ pip install celery[librabbitmq]

$ pip install celery[librabbitmq,redis,auth,msgpack]
以下是可用的捆绑：

### 序列化
celery[auth]:	使用 auth 序列化。
celery[msgpack]:
 	使用 msgpack 序列化。
celery[yaml]:	使用 yaml 序列化。

### 并发
celery[eventlet]:
 	使用 eventlet 池。
celery[gevent]:	使用 gevent 池。
celery[threads]:
 	使用线程池。
 	
### 传输和后端
celery[librabbitmq]:
 	使用 librabbitmq 的 C 库.
celery[redis]:	使用 Redis 作为消息传输方式或结果后端。
celery[mongodb]:
 	使用 MongoDB 作为消息传输方式（ 实验性 ），或是结果后端（ 已支持 ）。
celery[sqs]:	使用 Amazon SQS 作为消息传输方式（ 实验性 ）。
celery[memcache]:
 	使用 memcache 作为结果后端。
celery[cassandra]:
 	使用 Apache Cassandra 作为结果后端。
celery[couchdb]:
 	使用 CouchDB 作为消息传输方式（ 实验性 ）。
celery[couchbase]:
 	使用 CouchBase 作为结果后端。
celery[beanstalk]:
 	使用 Beanstalk 作为消息传输方式（ 实验性 ）。
celery[zookeeper]:
 	使用 Zookeeper 作为消息传输方式。
celery[zeromq]:	使用 ZeroMQ 作为消息传输方式（ 实验性 ）。
celery[sqlalchemy]:
 	使用 SQLAlchemy 作为消息传输方式（ 实验性 ），或作为结果后端（ 已支持 ）。
celery[pyro]:	使用 Pyro4 消息传输方式（ 实验性 ）。
celery[slmq]:	使用 SoftLayer Message Queue 传输（ 实验性 ）。