今天配置了一下yii2 的路由，用 /index.php?r=... 这样的路由，实在是不太习惯，所以我便试着把yii2 的路由，写成laravel 那般，以下为详情

1.环境介绍

　　lnmp php5.6, mysql5.5, lnmp1.2 

　　yii2-advanced

 

2.在 frontend/config/main.php 中，添加以下内容 

 
```
'urlManager' => [
            'enablePrettyUrl' => true,　　//开启URL美化 
            'showScriptName' => false,　　//禁用index.php文件 
            'rules' => require_once '../config/routes.php',   //载入路由设置文件 routes.php           

        ],

```
 

3.书写 routes.php 文件，之所以使用文件这样的格式，是为了避免main.php 文件过于冗余
```
<?php
return [
    'test.json' => 'demo/test',                 //未指定请求方式是，可以为如何方式，类似laravel 中的 any

    'POST api-post' => 'demo/post-test',        //POST 表示用post 方式请求， actionPostTest ==> post-test

    'get-demo/<id:\d+>' => 'demo/get-id',       //<id:\d+>  表示url中传递参数 id=??
];
　　
```
 

- api/test/test.json 为访问的url链接，demo/test 对应的是 控制器 DemoController 的 actionTest 方法

- 至于该routes.php 更多的用法，可以参考 laravel 的路由设置，在结合yii2 来进行

 

4. 编写 DemoController 控制器
```php
<?php
namespace frontend\controllers;

use Yii;
use yii\web\Controller;


/**
 * Site controller
 */
class DemoController extends Controller{

    public $layout = false; //不使用布局
    public  $enableCsrfValidation=false;

    //any www.yii2.com/test.json
    public function actionTest()
    {
        echo json_encode(['name'=>'zeopean']);
    }

    //post www.yii2.com/api-post
    public function actionPostTest()
    {
        echo json_encode(['name'=>'zeopean', 'method'=>'post']);

    }

    //any www.yii2.com/get-demo/12
    public function actionGetId()
    {
        $request = Yii::$app->request;
        $id = $request->get('id');
        echo json_encode(['id'=>$id]);
    }
}
　　
```
 

5. 如果你以为这样就可以运行，那就错了，你还需要在我们的nginx 中稍作配置，具体如下

        location / {
                if (!-e $request_filename){
                rewrite ^/(.*) /index.php last;
                }
        }

6. url的使用

- \Yii :: $app->urlManager 的使用

```
echo \Yii::$app->urlManager->createUrl(['site/page', 'id' => 'about']);
// /index.php/site/page/id/about/

echo \Yii::$app->urlManager->createUrl(['date-time/fast-forward', 'id' => 105])
// /index.php?r=date-time/fast-forward&id=105

echo \Yii::$app->urlManager->createAbsoluteUrl('blog/post/index');
// http://www.example.com/index.php/blog/post/index/

```

- yii\helpers\Url 的使用
```
use yii\helpers\Url;
 
// 当前活动路由
// /index.php?r=management/default/users
echo Url::to('');
 
// 相同的控制器，不同的动作
// /index.php?r=management/default/page&id=contact
echo Url::toRoute(['page', 'id' => 'contact']);
 
 
// 相同模块，不同控制器和动作
// /index.php?r=management/post/index
echo Url::toRoute('post/index');
 
// 绝对路由，不管是被哪个控制器调用
// /index.php?r=site/index
echo Url::toRoute('/site/index');
 
// 区分大小写的控制器动作 `actionHiTech` 的 url 格式
// /index.php?r=management/default/hi-tech
echo Url::toRoute('hi-tech');
 
// 控制器和动作都区分大小写的 url，如'DateTimeController::actionFastForward' ：
// /index.php?r=date-time/fast-forward&id=105
echo Url::toRoute(['/date-time/fast-forward', 'id' => 105]);
 
//  从别名中获取 URL 
// http://google.com/
Yii::setAlias('@google', 'http://google.com/');
echo Url::to('@google');
 
// 获取当前页的标准 URL 
// /index.php?r=management/default/users
echo Url::canonical();
 
// 获得 home 主页的 URL
// /index.php?r=site/index
echo Url::home();
 
Url::remember() ; //  保存URL以供下次使用

Url::previous(); // 取出前面保存的 URL 

```
 好了，这样就可以了