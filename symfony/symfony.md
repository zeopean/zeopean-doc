

#### symfony 返回json 数据

```
<?php

namespace AppBundle\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\JsonResponse;
use Symfony\Component\HttpFoundation\Response;

class ApiController extends Controller
{

    /**
     *  @Route("/lucky/number")
     */
    public function numberAction()
    {
        $number = rand(0, 100);
        $data = ['name'=>'zeopean', 'demo'=>'symfony'];
        #方法 1
//        return new Response(
//            json_encode($data),
//            200,
//            array('Content-Type' => 'application/json')
//        );
        
        ＃方法 2
        return new JsonResponse($data);

    }
}

```



#### symfony 视图

- 变量使用
```
    {{ ... }}
```
- 逻辑使用
```
    {% ... %}
```
- 注释
``` 
    {# ... #}
```

- 变量分配
```
$this->render('default/index.html.twig', array(
    'variable_name' => 'variable_value',
));
```

- 模板继承
```
{% extends 'base.html.twig' %}

```
- 使用asset加载静态文件
```
＃相对路径
<img src="{{ asset('images/logo.png') }}" alt="Symfony!" />
 
<link href="{{ asset('css/blog.css') }}" rel="stylesheet" />


＃绝对路径
<img src="{{ absolute_url(asset('images/logo.png')) }}" alt="Symfony!" />
```

- 使用block加载

```
{% block stylesheets %}
    <link href="{{ asset('css/main.css') }}" rel="stylesheet" />
{% endblock %}

{% block javascripts %}
    <script src="{{ asset('js/main.js') }}"></script>
{% endblock %}

```



#### 参数绑定器

```
$response->setParameter('foo', 'bar1'); //设置参数
$response->setParameter('foo', 'bar2', 'my/name/space'); //第三个参数表示命名空间

echo $response->getParameter('foo');    //获取参数
// => 'bar1'

echo $response->getParameter('foo', null, 'my/name/space');
// => 'bar2'

```

##### 给类增加参数存储器

```

class MyClass
{
    protected $parameter_holder = null;
    public function initialize ($parameters = array())
    {
        $this->parameter_holder = new sfParameterHolder();
        $this->parameter_holder->add($parameters);
    }
    public function getParameterHolder()
    {
        return $this->parameter_holder;
    }
}

```


#### 常量

- symfony使用自己的配置对象，称作sfConfig，用来取代常量

```
// symfony 使用sfConfig对象

sfConfig::set('sf_foo', 'bar');     //设置

echo sfConfig::get('sf_foo');       //获取值

```