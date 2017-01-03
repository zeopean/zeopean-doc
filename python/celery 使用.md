Celery 也定义了一组用于安装 Celery 和给定特性依赖的捆绑。

你可以在 requirements.txt 中指定或在 pip 命令中使用方括号。多个捆绑用逗号分隔。

```
$ pip install celery[librabbitmq]

$ pip install celery[librabbitmq,redis,auth,msgpack]
```

#celery 并发

```

#开始
celery multi start w1 -A task -l info

＃重启
celery multi restart w1 -A task -l info

＃停止
celery multi stop w1 -A task -l info
celery multi stopwait w1 -A task -l info

```

#celery 函数调用

```
#demo-function-name  add

#同步调用
result = add.delay(1, 2)

＃异步调用
result = add.apply_async((3, 2))

＃获取调用结果值
result.get() 

＃获取id
result.id 

＃判断值是否获取失败
result.failed()

＃判断值是否获取成功
result.successful()

＃判断值是否获取状态
result.state

#获取结果集
res = app.AsyncResult('33a27337-f7e5-40a2-9a4a-09848f244cec')
res.state   //SUCCESS

```

#subtask 子函数

```
#语法
add.subtask((2, 2), countdown=10)

＃简写
add.s(2, 2)


```

#groups 使用

```

from celery import group
from task import add

g = group(add.s(i) for i in xrange(10))
g(10).get()




```


#chains [管道]

```
from celery import chain
from task import add, mul

chain(add.s(4, 4) | mul.s(9) )().get()


```


#配置文件加载

```
#demo-1
from celery import Celery 

app = Celery()
app.config_from_object('config')




#demo-2
from celery import Celery
app = Celery()

import config
app.config_from_object(config)




#demo-3
from celery import Celery

app = Celery()

class Config:
    CELERY_ENABLE_UTC = True
    CELERY_TIMEZONE = 'Europe/London'

app.config_from_object(Config)


```


# 通过环境变量获取配置文件

```
import os
from celery import Celery

os.environ.setdefault('CELERY_CONFIG_MODULE', 'config')

app = Celery()
app.config_from_envvar('CELERY_CONFIG_MODULE')



```



# 日志的使用

```
from celery.utils.log import get_task_logger
logger = get_task_logger(__name__)

app = Celery()

@app.task
def add(x, y):
	logger.info('hello logger info')
	return x+y


```