
### WorkerMan已经支持的协议
WorkerMan目前已经支持HTTP、websocket、text协议(见附录说明)、frame协议(见附录说明)，ws协议(见附录说明)，需要基于这些协议通讯时可以直接使用，使用方法及时在初始化Worker时指定协议，例如
    
```

    use Workerman\Worker;
    // websocket://0.0.0.0:2345 表明用websocket协议监听2345端口
    $websocket_worker = new Worker('websocket://0.0.0.0:2345');
    
    // text协议
    $text_worker = new Worker('text://0.0.0.0:2346');
    
    // frame协议
    $frame_worker = new Worker('frame://0.0.0.0:2347');
    
    // tcp Worker，直接基于socket传输，不使用任何应用层协议
    $tcp_worker = new Worker('tcp://0.0.0.0:2348');
    
    // udp Worker，不使用任何应用层协议
    $udp_worker = new Worker('udp://0.0.0.0:2349');
    
    // unix domain Worker，不使用任何应用层协议
    $unix_worker = new Worker('unix:///tmp/wm.sock');
    
```

### 协议接口说明
在WorkerMan中开发的协议类必须实现三个静态方法，input、encode、decode，协议接口说明见Workerman/Protocols/ProtocolInterface.php，定义如下：

```php
namespace Workerman\Protocols;

use \Workerman\Connection\ConnectionInterface;

/**
 * Protocol interface
* @author walkor <walkor@workerman.net>
 */
interface ProtocolInterface
{
    /**
     * 用于在接收到的recv_buffer中分包
     *
     * 如果可以在$recv_buffer中得到请求包的长度则返回整个包的长度
     * 否则返回0，表示需要更多的数据才能得到当前请求包的长度
     * 如果返回false或者负数，则代表错误的请求，则连接会断开
     *
     * @param ConnectionInterface $connection
     * @param string $recv_buffer
     * @return int|false
     */
    public static function input($recv_buffer, ConnectionInterface $connection);

    /**
     * 用于请求解包
     *
     * input返回值大于0，并且WorkerMan收到了足够的数据，则自动调用decode
     * 然后触发onMessage回调，并将decode解码后的数据传递给onMessage回调的第二个参数
     * 也就是说当收到完整的客户端请求时，会自动调用decode解码，无需业务代码中手动调用
     * @param ConnectionInterface $connection
     * @param string $recv_buffer
     */
    public static function decode($recv_buffer, ConnectionInterface $connection);

    /**
     * 用于请求打包
     *
     * 当需要向客户端发送数据即调用$connection->send($data);时
     * 会自动把$data用encode打包一次，变成符合协议的数据格式，然后再发送给客户端
     * 也就是说发送给客户端的数据会自动encode打包，无需业务代码中手动调用
     * @param ConnectionInterface $connection
     * @param mixed $data
     */
    public static function encode($data, ConnectionInterface $connection);
}  
```