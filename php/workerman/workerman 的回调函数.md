
### workerman 的回调函数

```
<?php
/**
 * Created by PhpStorm.
 * User: zeopean
 * Date: 2016-08-26
 * Time: 17:18
 */
use Workerman\Worker;
require_once "../Workerman/Autoloader.php";

//Worker::$daemonize = true ;
$worker = new Worker("tcp://0.0.0.0:8888");

//设置reloadable
$worker->reloadable = true;    //不执行重载

//开始进程
$worker->onWorkerStart = function($worker)
{
    echo "Worker starting ... \n";
};

//Worker收到reload信号后执行的回调
$worker->onWorkerReload = function($worker)
{
    foreach ($worker->connections as $connection)
    {
        $connection->send("worker reloading! \n");
    }
};

//设置Workert停止时的回调函数
$worker->onWorkerStop = function($worker)
{
    echo "Worker stopping!!!\n";
};

//当有客户端连接时触发的回调函数
$worker->onConnect = function($connection)
{
  echo "new connection from ip ".$connection->getRemoteIp();
};

//当有客户端的连接上有数据发来时触发
$worker->onMessage = function($connection , $data)
{
    echo $data;
    $connection -> send("receive success!!");
};

//当客户端的连接断开时触发，不管连接是如何断开的，只要断开就会触发
$worker->onClose = function ($connection)
{
    echo "connection closed! \n";
};

//当连接的应用层发送缓冲区数据全部发送完毕时触发
$worker->onBufferFull = function($connection)
{
    echo "bufferFull and do not send ahain\n";
};

//onBufferFull 当连接的应用层发送缓冲区满时触发
$worker -> onBufferDrain = function($connection)
{
    echo "buffer drain and continue send \n" ;
};

// 当worker 发生错误时候调用
$worker -> onError = function($connection , $code , $msg)
{
    echo "error $code : $msg \n";
};

Worker::runAll();

```

