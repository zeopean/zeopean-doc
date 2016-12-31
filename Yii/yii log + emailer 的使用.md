今天试着把yii2 的日志，如果发送邮件的形式实现，具体实现如下

#### 1.环境介绍

　　lnmp php5.6, mysql5.5, lnmp1.2 

　　yii2-advanced
　　
#### 2.配置文件的编写

- 在frontend/config/main.php 添加mailer 和 log 的配置

```
    'mailer'    => require_once '../config/mail.php',
    'log'   => require_once '../config/log.php',

```

- mailer的配置如下(frontend/config/mail.php)
```
<?php
return [
    'class' => 'yii\swiftmailer\Mailer',
    'viewPath' => '@common/mail',
    'useFileTransport' => false,
    'transport' => [
        'class' => 'Swift_SmtpTransport',
        'host' => 'smtp.163.com',
        'username' => '**@163.com',
        'password' => '****',
        'port' => '25',
        'encryption' => 'tls',
    ],
    'messageConfig'=>[
        'charset'=>'UTF-8',
        'from'=>['zeopean@163.com'=>'zeopean']
    ],
];

```

- log的配置如下(frontend/config/log.php)
```

<?php
return [
    'traceLevel' => YII_DEBUG ? 3 : 0,
    'targets' => [
        [
            'class' => 'yii\log\EmailTarget',
            'levels' => ['error','info'],
            'categories' => ['email_log'],      #该email_log 会在日志方法使用时使用到
            'message' => [
                'from' => ['**@163.com'],
                'to' => ['**@qq.com'],
                'subject' => 'Database errors at example.com',
            ],
        ],
        [
            'class' => 'yii\log\FileTarget',
            'levels' => ['error', 'warning'],
        ],
    ],
];

```

#### 3.路由编写
```
#(frontend/config/routes.php)

return ['GET log-test'  => 'demo/log-test'];

```

#### 4.控制器编写

```
<?php
namespace frontend\controllers;

use Yii;
use yii\debug\models\search\Log;
use yii\log\EmailTarget;
use yii\web\Controller;


/**
 * Site controller
 */
class DemoController extends Controller{

    public $layout = false; //不使用布局
    public  $enableCsrfValidation=false;
    
    /**
     * ======================================================================
     * 测试日志生成 - 发送邮件
     */
    public function actionLogTest()
    {
        Yii::info("logging info", 'email_log');
    }
}


```
