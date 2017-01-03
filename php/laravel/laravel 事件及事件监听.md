以下是我对事件使用的一些记录

##### 创建事件
执行以下命令，执行完成后，会在 app\Events 下面出现一个 DeleteEvent.php 文件，事件就在次定义
```
php artisan make:event DeleteEvent


```

##### 编写事件
```php
#DeleteEvent.php
<?php

namespace App\Events;

use App\Events\Event;
use Illuminate\Queue\SerializesModels;
use Illuminate\Contracts\Broadcasting\ShouldBroadcast;

class DeleteEvent extends Event
{
    use SerializesModels;

    public function __construct()
    {
        //
    }

    public function broadcastOn()
    {
        print 'delete event';
    }
}



```


##### 创建监听listener
执行以下命令，执行完成后，会在 app\Listeners 下面出现一个 DeleteEventListener.php 文件，是对事件 DeleteEvent的监听
```
php artisan make:listener --event=DeleteEvent  DeleteEventListener

```

##### 编写事件监听
```php
#DeleteEventListener.php
<?php

namespace App\Listeners;

use App\Events\DeleteEvent;
use Illuminate\Queue\InteractsWithQueue;
use Illuminate\Contracts\Queue\ShouldQueue;

class DeleteEventListener
{
    public function __construct()
    {
        //
    }

    public function handle(DeleteEvent $event)
    {
        //
        $event->broadcastOn();
    }
}



```


##### 调用事件-在控制器使用
```php
#EventController.php
<?php

namespace App\Http\Controllers;

use App\Events\DeleteEvent;
use App\Events\SomeEvent;
use Illuminate\Http\Request;

use App\Http\Requests;

class EventController extends Controller
{
    //
    public function index()
    {
//        event(new SomeEvent());       //框架默认调用broadcastOn()

        $event = new DeleteEvent();     //自定义 
        event($event->broadcastOn());
    }
}

```

##### 编写路由

```
#routes.php
Route::get('/event',['uses'=>'EventController@index']);

```

