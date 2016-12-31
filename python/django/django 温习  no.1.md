
#### 查看django版本
```
    python -c "import django;print(django.get_version())"
```

#### django 创建项目
```

django-admin startproject app_name
```


#### 数据库配置
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'django18',
        'USER': 'admin',
        'PASSWORD': 'admin',
        'HOST': '192.168.31.10',
        'PORT': '3306',
    }
}

```

#### 进行数据迁移
```
python manage.py mrigate

```

#### 模型的使用

```
# query-sql 的使用
Model_name.objects.raw('sql-str %s ', [str])

#获取所有
Model_name.objects.all()

#get
Model_name.objects.get()

#条件查询
Model_name.objects.filter()





```




#### 运行服务
```
python manage.py runserver
```

#### 项目迁移操作
```
#创建子app
python manage.py startapp polls

#可以在models.py中创建数据模型，并执行以下迁移操作
python manage.py makemigrations polls

#同步到数据库
python manage.py migrate

#查看创建到sql
python manage.py sqlmigrate polls 0001

```

#### django api
```
python manage.py shell

```

#### 创建管理员账号
```
python manage.py createsuperuser
```

#### 路由配置
在urls.py 文件中进行配置 urlpatterns

```
#app/urls.py 默认urls 设置
from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    url(r'^polls/', include('polls.urls', namespace='polls')),
    url(r'^admin/', include(admin.site.urls)),
]



#polls/urls.py 模块urls
from django.conf.urls import url
from . import views


urlpatterns = [

    url(r'^$', views.index, name='index'),
    url(r'^(?P<question_id>[0-9]+)/$', views.detail, name='detail'),
    url(r'^(?P<question_id>[0-9]+)/results/$', views.results, name='results'),
    url(r'^(?P<question_id>[0-9]+)vote/$', views.vote, name='vote'),

    url(r'^get-model.page$', views.get_model, name='get_model'),
    url(r'^get-detail.page/(?P<question_id>[0-9]+)$', views.get_detail, name='get_detail'),
    url(r'^get-detail-404.page/(?P<question_id>[0-9]+)$', views.get_detail_404, name='get_detail_404'),


]

```

#### 视图的使用
```

from .models import Question                            #使用模型
from django.template import RequestContext, loader
from django.http import Http404                         #404 错误处理页面
from django.shortcuts import render, get_object_or_404  #页面跳转，404错误处理


from django.http import HttpResponse                    #响应页面

def index(request):
    question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')  #定义模板
    context = RequestContext(request, {                 #请求
        'question_list' : question_list,                #返回数据
    })
    return HttpResponse(template.render(context))       #页面响应


def get_model(requesti):
    question_list = Question.objects.order_by('-pub_date')[:5]      #模型使用
    output = ', '.join([p.question_text for p in question_list])    #数据处理
    return HttpResponse(output)

def get_detail(request, question_id):
    try:                                                            #异常处理
        question = Question.objects.get(pk=question_id)             #数据模型处理
    except Question.DoesNotExist:                           
        raise Http404("Question does not exist!")                   #异常处理
    return render(request, 'polls/detail.html', {'question':question})  #页面响应


def get_detail_404(request, question_id):
    question = get_object_or_404(Question, pk=question_id)          #数据处理 或者 404错误处理
    return render(request, 'polls/detail.html', {'question':question})  #响应



```

#### 返回json数据

```
from django.http import JsonResponse

def shirt(request):
    shirt = Shirt(name='zeopean shirt', shirt_size="L")
    shirt.save()
    return JsonResponse({
        'code' : '200',
        'msg'  : 'success'
    })

```

#### 模板文件的使用
```

{{ args_name }}     #变量明

{% func_call %}     #使用函数

{% for %} {% endfor %}

{% if %} {% else %} {% endif %}

{% url 'namespace:action' request_params %}



```


#### django 测试模块

```
python manage.py test polls

```



