
flask 作为一个python web 框架，还是很有学习意义的，接下来介绍下他的使用

#### 创建app项目 及目录
    
    ./app
        static
        templates
            base.html
            foreach.html
            index.html
        __init__.py         #初始化py
        views.py            #视图
    ./tmp
    run.py                  #run.py

#### 编写init
```py
from flask import Flask

app = Flask(__name__)
from app import views
```

#### 编写views
```py
from flask import render_template
from app import app

@app.route('/')
@app.route('/index')
def index():
    user = {'username' : 'zeopean'}
    return render_template('index.html' , user=user)

@app.route('/foreach')
def foreach():
    posts = [
        {
            'author' : { 'nickname' : 'zeopean' },
            'body'   : 'beautiful day in Portland!'
        },
        {
            'author' : {'nickname'  : 'daming'},
            'body'   : 'I am Daming!'
        }
    ]

    return render_template('foreach.html' ,
                           title = 'Foreach',
                           posts = posts
                           )
```

#### 编写run
```py
from app import app

app.run(debug=True)


```

## flask views中的便签

#### 模版继承
```py
{% extends 'base.html' %}

```

#### for
```
{% for post in posts %}

{% endfor %}
```

#### if
```
{% if a > 0 %}

{% else %}

{% endif %}
```
#### 使用变量
```
{{ user.name }}
```

### response && request

#### 返回json（jsonify） 

```
from flask import jsonify

---

@app.route('/api',methods=['get'])
def api():
    return jsonify({'name':'zeopean' , 'age':21});
    
```

#### 获取参数

- request.args.get('name')

    request.args 这个属性用于表示 GET 请求在 URL 上附带的参数


- json.loads(request.data)

    request.data 这个属性用于表示 POST 等请求的请求体中的数据
