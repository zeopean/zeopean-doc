
#### 具体属性见代码
```php
<?php
/**
 * Created by PhpStorm.
 * User: zeopean
 * Date: 2016-08-26
 * Time: 16:35
 */

use Workerman\Worker;
use Workerman\Lib\Timer;
require_once "../Workerman/Autoloader.php";

Worker::$daemonize = true;      //该进程为 守护进程

Worker::$stdoutFile = '/tmp/worker.log';    //打印输出到指定文件

Worker::$pidFile = '/tmp/workerman.pid';//设置WorkerMan进程的pid文件路径 不建议使用

Worker::$logFile = '/tmp/worker1.log';  //设置workerman日志文件位置

$worker = new Worker("tcp://0.0.0.0:8585");
$worker -> count = 4;                           // 设置进程数
$worker -> name = 'myWorker-zp';                //设置进程名字
$worker -> user = 'www';                        //设置运行用户

$worker -> reloadable = true ;                  //设置此实例收到reload信号后是否reload重启

$worker -> transport  = 'udp';                  //设置实例使用的传输协议 tcp | udp

$worker -> onWorkerStart = function($worker){   //启动进程
    if($worker -> id === 0)
    {
        Timer::add(1 , function(){              //使用定时器
            $time = time();

            echo "worker id 为0 时，打印！======> $time \n";
        });

        Timer::add(10 , function() use ($worker){
            // 遍历当前进程所有的客户端连接，发送当前服务器的时间
           foreach($worker->connections as $connection)
           {
                $connection -> send(time());
           }
        });
    }
};

Worker::runAll();

```