
#### 数据字段类型
```
IntegerField()      整型

CharField()         字符型

DateField()         日期时间型

BooleanField()      bool类型

ForeignKeyField()   外键

```

#### 创建连接
```
db.create_connect()
```


#### 创建表
```
db.create_table(..)
db.create_tables([...])
```

#### 新增数据
```
Person.create(name='name')

```


#### 保存数据
```
person = Person(name='name')
person.save()

```



#### 删除数据

```
person.delete_instance()

```



#### 查询单条数据

```

person = Person.select().where(Person.name='name').get()

#简写
person = Person.get(Person.name='name')

```


#### 查询所有数据

```

Person.select()

```

#### 排序
```

Person.select().order_by(Person.id)     

Person.select().order_by(Person.id).desc()

```

