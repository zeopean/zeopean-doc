
#### 开发环境配置
再使用 mongodb 之前，需要先安装 pymongo ，以及flask_mongoengine

```
1. 切换到 virtualenv 环境

    . /pyenv/bin/activate
    
2. 安装pymongo
    
    pip install pymongo

3. 安装flask_mongoengine

    pip install flask_mongoengine

```

#### 书写model

```
from flask_mongoengine import MongoEngine

#--

#进行配置
app.config['MONGODB_SETTINGS'] = {
    'db'    : 'the_way_to_flask',
    'host'  : 'localhost',
    'port'  : 27017
}

＃创建mongo原型
mdb = MongoEngine()
mdb.init_app(app)

class Address(mdb.Document):
    name = mdb.StringField()
    address = mdb.StringField()
    
    # 查询 Address.objects(name="zhangsan").first()
    # 添加 Address(name='lisi', address='lisi@gmail.com').save()
    # 删除 Address.delete()
    # 更新 Address.update(name="lisi@outlook.com")

```



#### 书写视图

views.py
```
from models import Address
from flask import jsonify

#--

@app.route('/mdb_list',methods=['get'])
def mdb_list():
    name = request.args.get('name')
    address = request.args.get('address')
    Addr = Address.objects(name=name,address=address).first()

    if not Addr:
        Address(name=name , address=address).save()
        return jsonify({'code':1,'message':'success'})
    else:
        return jsonify(Addr.to_json())

```







