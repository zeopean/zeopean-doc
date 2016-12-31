#### symfony 在控制器定义路由

```
@Route("/lucky/number")     #必须用双引号

@Route("/api/get-lucky-number/{number}")  #{number} 为传参


```
##### routing.yml 配置路由

```
api:
    path:     /api/{_locale}/{year}/{title}.{_format}
    defaults: {_controller: AppBundle:Api:getJson, _format:html}
    requirements:
        _locale: en|fr
        _format: html|rss
        year:    \d+
    schemes:  [http]
show:
    path:     /show.json
    defaults:  {_controller: AppBundle:Api:showUrl}
    schemes:  [http]

tpl:
    path:     /lucky/number
    defaults: {_controller:AppBundle:Api:number}
    schemes:  [http]

```
- api   ： 表示该理由的别名，在 使用控制器使用 generate && generateUrl 可以使用到

- path  ： 表示访问到url ，其中参数可以用｛｝传递 ，传递到参数可以在 控制器中动作参数使用

- defaults   ： 表示对应到控制器及方法，APPBundle 表示控制器所在目录，Api 表示控制器，getJson 表示请求方法

- requirements : 表示参数到验证方式，其中 ｜ 表示 ‘或’, \d+ 为匹配一个数字

- schemes   : 表示对应到请求模式，http ｜ https

##### 下面介绍下在控制器中，如何使用这样到router

```
    # $year,$title 就是｛｝中到参数, $_controller 表示控制器, $_route 对应别名 api，show， tpl
    public function getJsonAction($title, $year, $_locale, $_format, $_controller, $_route)
    {
        $numbers = [];
        for ($i = 0; $i < 10; $i++)
        {
            $numbers[] = rand(0, 100);
        }
        $other = ['title' => $title, 'year' => $year, '_locale' => $_locale, '_format' => $_format, '_controller' => $_controller, '_route' => $_route];
        return  new JsonResponse($other);
    }
    
    /**
       #运行结果
        {
            title: "api",
            year: "2014",
            _locale: "en",
            _format: "html",
            _controller: "AppBundle\Controller\ApiController::getJsonAction",
            _route: "api"
        }
        
    */

    public function showUrlAction()
    {
        //获取对应的url
        $params = $this->get('router')->match('/lucky/number');

        //生成uri
        $uri = $this->get('router')->generate('api', [
            'year'  => '2022',
            'title' => 'en',
        ]);

        //生成带域名的url
        $url = $this->generateUrl('api', [
            'year'  => '2022',
            'title' => 'fr',
            '_format'   => 'html'
        ], UrlGeneratorInterface::ABSOLUTE_URL);
//        $uri = '';
        return new JsonResponse(['params' => $params, 'uri' => $uri, 'url' => $url]);

    }
    
    /**
        {
            params: {
            _controller: "AppBundle\Controller\ApiController::numberAction",
            _route: "app_api_number"
            },
            uri: "/api/en/2022/en",
            url: "http://127.0.0.1:8000/api/en/2022/fr"
        }
    
    */

```
- $this->get('router')->generate('api' , ... ) 表示获取一个uri

- $this->generateUrl('api', , UrlGeneratorInterface::ABSOLUTE_URL) 则表示生成绝对到url





