


#### 模型定义

```
# models.py 编码

#encoding=utf8
from flask import Flask
from flask_mongoengine import MongoEngine

app = Flask(__name__)
#mongodb 数据库配置
app.config['MONGODB_SETTINGS'] = {
    'db'    : 'flask',
    'host'  : 'localhost',
    'port'  : 27017
}

mdb = MongoEngine()
mdb.init_app(app)

class Address(mdb.Document):
    name = mdb.StringField()
    address = mdb.StringField()

    #添加 Address(name='lisi', address='lisi@gmail.com').save()
    #查询 Address.objects(name="zhangsan").first()
    #删除 Address.delete()
    #更新 Address.update(name="lisi@outlook.com")


class User(mdb.Document):
    username = mdb.StringField()
    password = mdb.StringField()
    email    = mdb.StringField()

    def to_json(self):
        return {"username": self.username,
                "password": self.password}
    #当前用户是否被授权，因为我们登陆了就可以操作，所以默认都是被授权的
    def is_authenticated(self):
        return True

    #用于判断当前用户是否已经激活，已经激活的用户才能登陆
    def is_active(self):
        return True

    #用于判断当前用户是否是匿名用户，很明显，如果这个用户登陆了，就必须不是
    def is_anonymous(self):
        return False

    #获取改用户的唯一标示
    def get_id(self):
        return str(self.id)

```


#### 发送登录请求
```
#!encoding=utf-8

# views.py

@app.route('/api_login' ,methods=['POST'])
def api_login():
    username = request.args.get('username')
    password = request.args.get('password')

    user = User.objects(username=username ,
                        password=password).first()

    if user:
        login_user(user)
        return jsonify(user.to_json())

    else:
        return jsonify({'code':'-1' , 'message':'error message'});

```

#### 登出操作
```
@app.route('/logout',methods=['get','post'])
def logout():
    logout_user()
    return jsonify(**{
        'code':'1',
        'message':'logout ok!'
    })
    
```

#### 获取当前登录用户
```
# views.py

@app.route('/get_user',methods=['get', 'post'])
def get_user():
    if current_user.is_authenticated:
        resp = {
            'code':1,
            'message':'current user',
            'data':current_user.to_json()
        }
    else:
        resp = {
            'code':0,
            'message':'none current user'
        }
    return jsonify(**resp)
    
```


#### 库说明
```
# views.py

from flask import render_template,flash,redirect,request
#载入程序
from app import app
from .forms import LoginForm
from app import db
#载入模型
from models import Users,Address,User
#载入json出来函数
from flask import jsonify
#用户登录 模块
from flask_login import login_user
from flask_login import login_required
#登出操作
from flask_login import logout_user
#获取当前用户
from flask_login import current_user
#获取 login_manager 对象
from app import login_manager

```







