
* 一直没发现laravel 控制起对于 Route 还有这样的功能，暂且记下，方便学习

1.路由缓存

创建：

        php artisan route:cache
清除：

        php artisan route:clear

需要注意的是，当我们创建了新的路由之后，一定要记得创新创建一次路由缓存


* 前段时间一直在弄 laravel5 的依赖注入，还整的自己不知所以的，今天看了文档中的控制器的依赖注入，呵呵，原来我以前就用过注入，真是被自己蠢哭了，哎....
* 下面开始介绍laravel 控制器中注入的使用
    
    * 构造器注入
    
        <?php namespace App\Http\Controllers;
        use Illuminate\Routing\Controller;
        use App\Repositories\UserRepository;  ＃这是要注入的对象
        
        class UserController extends Controller {
        
            /**
             * 用户保存库实例。
             */
            protected $users;
            ＃ 在控制器构造器中，当作参数，在初始化时注入
            public function __construct(UserRepository $users)
            {
                $this->users = $users;
            }
        }    

    * 方法注入
        
        
        <?php namespace App\Http\Controllers;

        use Illuminate\Http\Request;
        use Illuminate\Routing\Controller;
        
        class UserController extends Controller {
        
            /**
             * 保存一个新的用户。
             *
             * @param  Request  $request
             * @return Response
             */
            public function store(Request $request)
            {
                $name = $request->input('name');
        
                //
            }
        
        }
       
