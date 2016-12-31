
### stream_set_blocking 的用法
```
    bool stream_set_blocking ( resource $stream , int $mode )
```

为 stream 设置阻塞或者阻塞模。

此函数适用于支持非阻塞模式的任何资源流（常规文件，套接字资源流等）。

#### 参数 

stream
资源流。

#### mode
    如果 mode 为0，资源流将会被转换为非阻塞模式；如果是1，资源流将会被转换为阻塞模式。
    该参数的设置将会影响到像 fgets() 和 fread() 这样的函数从资源流里读取数据。
    在非阻塞模式下，调用 fgets() 是会立即返回；而在阻塞模式下，将会一直等到从资源流里面获取到数据才能返回。
    
### stream_socket_client


stream_socket_client打开 internet 或 unix 域 socket 连接

#### 描述
```
    resource stream_socket_client ( string $remote_socket [, int &$errno [, string &$errstr [, float $timeout = ini_get("default_socket_timeout") [, int $flags = STREAM_CLIENT_CONNECT [, resource $context ]]]]] )
```

发起一个流或者报连接 remote_socket 所指定的目标.创建的 socket 的类型是由传输使用标准的 url 格式指定:传输 ://target .为 internet domain sockets(af_inet)如 tcp 和 udp .target remote_socket 部分的参数应包含一个hostname后面跟一个冒号和一个端口号或 ip 地址.对于 unix domain sockets ,目标系统上的部分应该指向 socket 文件.

##### 注:

缺省情况下,该流将在阻止模式下.可以将其切换到非阻塞模式使用 stream_set_blocking() .

#### 参数

    remote_socket
    要连接的地址到 socket
    
    errno
    不会将系统级别的错误,如果连接失败.
    
    errstr
    不会将系统级错误消息如果连接失败.
    
    超时
    连接之前等待的秒数()系统调用超时.
    
    注:此参数仅在未进行异步的连接企图.



#### 返回值

或者在失败时返回成功一个流,它可能与其他文件一起使用的函数(如 fgets ( )() , fgetss() , fflush() , fclose ( )() 和 feof() )或者在失败时返回 false .

errors/exceptions

在失败 errno 和 errstr 参数将被填充的实际系统级别的错误发生在系统级别的连接()的调用.如果 errno 中返回的值是0,函数返回 false .表示错误发生之前的连接.()的调用.这很可能是由于初始化 socket 的问题.注意, errno 并且 errstr 参数将始终是按引用传递的.

#### 示例

example #1stream_socket_client()示例

```
< ?php
    $fp = stream_socket_client("tcp://www.example.com:80", $errno, $errstr, 30);
    if (!$fp) {
    echo "$errstr ($errno) < br / > n";
    } else {
    fwrite($fp, "GET / HTTP/1.0rnHost: www.example.comrnAccept: */*rnrn");
    while (!feof($fp)) {
    echo fgets($fp, 1024);
    }
    fclose($fp);
    }
    ? >
```