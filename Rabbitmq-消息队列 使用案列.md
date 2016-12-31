
* 服务器端 code

        <?php
        $routingkey = 'key' ;
        //连接消息
        $conn_args = array(
            'host' => '127.0.0.1',
            'port' => '5672',
            'login' => 'guest',
            'password' => 'guest',
            'vhost'=>'/'
        );
        
        //创建连接
        $conn = new AMQPConnection($conn_args);
        if(!$conn -> connect())
        {
            die("don't connectint");
        }
        
        //发送的消息
        $message = json_encode(array('python' , 'php' , 'laravel','code'));
        //创建 channel
        $channel = new AMQPChannel($conn);
        // 创建 exchange
        $exchange = new AMQPExchange($channel);
        //创建名字
        $exchange->setName('exchange');
        $exchange->setType(AMQP_EX_TYPE_DIRECT);
        $exchange->setFlags(AMQP_DURABLE);
        
        echo "exchange status".$exchange->declareExchange();
        echo '<br>';
        for($i = 0 ; $i < 100 ; $i++)
        {
            if($routingkey == 'key2')
            {
                $routingkey = 'key';
            }else{
                $routingkey = 'key2';
            }
            $exchange->publish($message , $routingkey);
        }
        
        $exchange->publish($message , $routingkey);
        
        //创建队列
        $q = new AMQPQueue($channel);
        //设置队列名字
        $q -> setName('queue');
        $q -> setFlags(AMQP_DURABLE | AMQP_AUTODELETE);
        echo "queue status:".$q->declareQueue();
        echo '<br>';
        
        echo "queue bind:".$q->bind('exchange' , 'route.key');  //队列绑定到 routingkey 上面
        
        $channel->startTransaction();
        echo "send: " . $exchange->publish($message , "route.key");  //通过 routekey 发送消息
        $channel->commitTransaction();
        
        // 关闭连接
        $conn->disconnect();





* 客户端 code
 
        <?php

        $bindingKey = 'key2' ;
        
        //连接消息
        $conn_args = array(
            'host' => '127.0.0.1',
            'port' => '5672',
            'login' => 'guest',
            'password' => 'guest',
            'vhost'=>'/'
        );
        //创建连接
        $conn = new AMQPConnection($conn_args);
        $conn -> connect();
        
        
        //设置queue名称， 使用exchange ， 绑定routingKey
        $channel = new AMQPChannel($conn);
        //创建队列 queue
        $q = new AMQPQueue($channel);
        $q->setName('queue2');
        $q->setFlags(AMQP_DURABLE);
        $q->declareQueue();
        
        //进行绑定
        $q->bind('exchange' , $bindingKey);
        
        
        // 获取消息
        $messages = $q->get(AMQP_AUTOACK);
        if($messages)
        {
            var_dump(json_decode($messages->getBody()  , true));
        }
        //关闭连接
        $conn->disconnect();








