


### python ABC 模块


1. python assert 用作判断语句的真假,如果为假的话将触发AssertionError错误


2. py abc 模块的使用
	-- 2.1 注册abc 虚拟子类

#!/usr/bin/python env
#encoding=utf-8
#使用python 的虚拟子类

#先注册一个abc 虚拟子类
from abc import ABCMeta

#
class MyABC:
        __metaclass__ = ABCMeta


MyABC.register(tuple)

assert issubclass(tuple , MyABC)
assert isinstance(() ,MyABC)


### 2016-02-01  python 的 __class_method__ 类方法

1. __init__  类似于构造函数
#!/usr/local/bin/python
class Study:
        def __init__(self,name=None):
                self.name = name
        def say(self):
                print self.name
study = Study("Badboy")
study.say()

2.    __del__  类似于析构函数
#!/usr/local/bin/python
class Study:
        def __init__(self,name=None):
                self.name = name
        def __del__(self):
                print "Iamaway,baby!"
        def say(self):
                print self.name
study = Study("zhuzhengjun")
study.say()

3. __repr__ 
使用repr(obj)的时候，会自动调用__repr__函数，该函数返回对象字符串表达式，
用于重建对象，如果eval_r(repr(obj))会得到一个对象的拷贝。
```py
#!/usr/local/bin/python
class Study:
        def __init__(self,name=None):
                self.name = name
        def __del__(self):
                print "Iamaway,baby!"
        def say(self):
                print self.name
        def __repr__(self):
                return "Study('jacky')"
study = Study("zhuzhengjun")
study.say()
print type(repr(Study("zhuzhengjun"))) # str
print type(eval_r(repr(Study("zhuzhengjun")))) # instance
study = eval_r(repr(Study("zhuzhengjun")))
study.say()
```
4. __str__

    Python能用print语句输出内建数据类型。有时，程序员希望定义一个类，要求它的对象也能用print语句输出。
    
    Python类可定义特殊方法__str__，为类的对象提供一个不正式的字符串表示。如果类的客户程序包含以下语句：
    ```
    print objectOfClass
    ```
    那么Python会调用对象的__str__方法，并输出那个方法所返回的字符串。

```py
#!/usr/local/bin/python
class PhoneNumber:
        def __init__(self,number):
                 self.areaCode=number[1:4]
                 self.exchange=number[6:9]
                 self.line=number[10:14]
        def __str__(self):
                return "(%s) %s-%s"%(self.areaCode,self.exchange,self.line)
def test():
         newNumber=raw_input("Enter phone number in the form. (123) 456-7890: \n")
         phone=PhoneNumber(newNumber)
         print "The phone number is:"
         print phone
if__name__=="__main__":
         test()
```


5.__cmp __   比较运算符，0：等于 1：大于 -1：小于 
```py
class Study: 
     def __cmp__(self, other): 
         if other > 0 : 
             return 1 
         elif other < 0: 
             return - 1 
         else: 
             return 0 
study = Study() 
if study > -10:print 'ok1' 
if study < -10:print 'ok2' 
if study == 0:print 'ok3'

##
    打印：ok2 ok3
    说明:在对类进行比较时，python自动调用__cmp__方法，如-10 < 0 返回 -1，也就是说study 应该小与 -10，估打印ok2
```

6.__getitem__    它只是重定向到字典，返回字典的值。
```
class Zoo: 
     def __getitem__(self, key): 
         if key == 'dog':return 'dog' 
         elif key == 'pig':return  'pig' 
         elif key == 'wolf':return 'wolf' 
         else:return 'unknown' 
zoo = Zoo() 
print zoo['dog'] 
print zoo['pig'] 
print zoo['wolf']

# 打印 dog pig wolf
```

7.__setitem__    简单地重定向到真正的字典 self.data ，让它来进行工作。 
```
class Zoo: 
     def __setitem__(self, key, value): 
         print 'key=%s,value=%s' % (key, value) 
zoo = Zoo() 
zoo['a'] = 'a' 
zoo['b'] = 'b' 
zoo['c'] = 'c'

# 打印：
key=a,value=a
key=b,value=b
key=c,value=c
```

8. __delitem__

__delitem__ 在调用 del instance[key] 时调用，你可能记得它作为从字典中删除单个元素的方法。当你在类实例中使用 del 时，Python 替你调用
__delitem__ 专用方法。

```
class A: 
     def __delitem__(self, key): 
         print 'delete item:%s' %key 
a = A() 
del a['key']
```
### python 魔术方法

    C.__init__(self[, arg1, ...]) 构造器（带一些可选的参数）
    
    C.__new__(self[, arg1, ...]) 构造器（带一些可选的参数）通常用在设置不变数据类型的子类。
    
    C.__del__(self) 析构器
    
    C.__str__(self) 可打印的字符输出；内建str()及print 语句
    
    C.__repr__(self) 运行时的字符串输出 内建repr() 和‘‘ 操作符
    
    C.__unicode__(self) Unicode 字符串输出；内建unicode()
    
    C.__call__(self, *args) 表示可调用的实例
    
    C.__nonzero__(self) 为object 定义False 值 内建bool() （从2.2 版开始）
    
    C.__len__(self) “长度”（可用于类） 内建len()
    
    
    
    C.__cmp__(self, obj) 对象比较；内建cmp()
    
    C.__lt__(self, obj) 小于/小于或等于 对应<及<=操作符
    
    C.__gt__(self, obj) 大于/大于或等于 对应>及>=操作符
    
    C.__eq__(self, obj) 等于/不等于 对应==,!=及<>操作符
    
    
    
    
    C.__getattr__(self, attr) 获取属性 内建getattr() 仅当属性没有找到时调用
    
    C.__setattr__(self, attr, val) 设置属性
    
    C.__delattr__(self, attr) 删除属性
   
    C.__getattribute__(self, attr) a 获取属性；内建getattr() 总是被调用
   
    C.__get__(self, attr) a （描述符）获取属性
   
    C.__set__(self, attr, val) a （描述符）设置属性
   
    C.__delete__(self, attr) a （描述符）删除属性
   
   
   
    
    
    C.__*add__(self, obj) 加；+操作符
    
    C.__*sub__(self, obj) 减；-操作符
    
    C.__*mul__(self, obj) 乘；*操作符
    
    C.__*div__(self, obj) 除；/操作符
    
    C.__*truediv__(self, obj) e True 除；/操作符
    
    C.__*floordiv__(self, obj) e Floor 除；//操作符
    
    C.__*mod__(self, obj) 取模/取余；%操作符
    
    C.__*divmod__(self, obj) 除和取模；内建divmod()
    
    C.__*pow__(self, obj[, mod]) 乘幂；内建pow();**操作符
    
    C.__*lshift__(self, obj) 左移位；<<操作符
    
    
    
    
    
    C.__*rshift__(self, obj) 右移；>>操作符
    
    C.__*and__(self, obj) 按位与；&操作符
    
    C.__*or__(self, obj) 按位或；|操作符
    
    C.__*xor__(self, obj) 按位与或；^操作符
    
    
    
    
    C.__neg__(self) 一元负
    
    C.__pos__(self) 一元正
    
    C.__abs__(self) 绝对值；内建abs()
    
    C.__invert__(self) 按位求反；~操作符
    
    
    
    
    C.__complex__(self, com) 转为complex(复数);内建complex()
    
    C.__int__(self) 转为int;内建int()
    
    C.__long__(self) 转为long；内建long()
    
    C.__float__(self) 转为float；内建float()
    
    
    
    
    C.__oct__(self) 八进制表示；内建oct()
    
    C.__hex__(self) 十六进制表示；内建hex()
    
    
    
    
    C.__coerce__(self, num) 压缩成同样的数值类型；内建coerce()
    
    C.__index__(self)g 在有必要时,压缩可选的数值类型为整型（比如：用于切片
    
    
    
    
    
    C.__len__(self) 序列中项的数目
    
    C.__getitem__(self, ind) 得到单个序列元素
    
    C.__setitem__(self, ind,val) 设置单个序列元素
    
    C.__delitem__(self, ind) 删除单个序列元素
    
    
    
    
    
    C.__getslice__(self, ind1,ind2) 得到序列片断
    
    C.__setslice__(self, i1, i2,val) 设置序列片断

    C.__delslice__(self, ind1,ind2) 删除序列片断

    C.__contains__(self, val) f 测试序列成员；内建in 关键字

    C.__*add__(self,obj) 串连；+操作符

    C.__*mul__(self,obj) 重复；*操作符

    C.__iter__(self) e 创建迭代类；内建iter()


    
    
    C.__len__(self) mapping 中的项的数目

    C.__hash__(self) 散列(hash)函数值

    C.__getitem__(self,key) 得到给定键(key)的值

    C.__setitem__(self,key,val) 设置给定键(key)的值

    C.__delitem__(self,key) 删除给定键(key)的值

    C.__missing__(self,key) 给定键如果不存在字典中，则提供一个默认值

