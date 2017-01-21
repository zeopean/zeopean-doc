




#### % 的使用

```
#统计时长
a = np.arange(1000)
%timeit a**2


```

#### ? 的使用

```
np.array?

```



#### 设置俩个时间的时间差

```
datetime.timedelta对象代表两个时间之间的的时间差，两个date或datetime对象相减时可以返回一个timedelta对象。
 
构造函数：
class datetime.timedelta([days[, seconds[, microseconds[, milliseconds[, minutes[, hours[, weeks]]]]]]])
所有参数可选，且默认都是0，参数的值可以是整数，浮点数，正数或负数。
 
内部只存储days，seconds，microseconds，其他参数的值会自动按如下规则抓转换：
 
1 millisecond（毫秒） 转换成 1000 microseconds（微秒）
1 minute 转换成 60 seconds
1 hour 转换成 3600 seconds
1 week转换成 7 days

```


#### staticmethod && classmethod 
- 静态方法 和 类方法的使用

```
class C(object):
    @staticmethod
    def func():
        ...
        
class A(object):
    @classmethod
    def func():
        ...


```

#### python 的链式操作

```
class Person:

    def name(self, value):
        self.name = value
        return self

    def age(self, value):
        self.age = value
        return self

    def intro(self):
        print "hello ",self.name," Your age is ",self.age

person = Person()
person.name('zeopean').age(23).intro()

```


#### 代码优化

- 使用 join 代替 ＋

``` 
>>>li = ['my','name','is','bob'] 
>>>' '.join(li)    #用空格把列表连接起来，所以就成了一个字符串了
'my name is bob' 
```

- 使用 format 代替 ％
```
>>> print "{} is {}".format('zeopean','body')
zeopean is body
```
 

- 使用enumerate 遍历数据


#### 异常处理格式
```
try:

except <name>:
    
except (name1, name2):
    # 发生 name1 ｜ name2 中的任意一个异常
except <name> as <data>:
    # 获取对象实例
except:
    # 异常时执行
else:
    # 无任何异常时执行
finally:
    # 不管有无异常都会执行


```




#### enumerate 遍历数组
```
li = ['1', 'b', 'c', 'e']
for i, e in enumerate(li):
    print i
    
'''
def enumerate(sequence, start=0):
    n = start
    for elem in sequence:
        yield n, elem
        n += 1
'''

```



#### time 

    time.time()     #获取时间戳
    time.ctime()    #获取一个时间字符串
    
    
#### fileinput  文件输入
```py
#!/usr/bin/env python3 
import fileinput 
#filein.py
with fileinput.input() as f_input:
    for line in f_input:
        print(line , end='')
        
# 切换到文件当前目录，并执行  
	 $   ls .. | python3 filein.py          #执行
	 $  python3 filein.py < /etc/passwd     
```

#### 程序输出、退出
```
import sys
sys.stderr.write(“It failed \n”)    #写入
raise SystemExit(1)                 #程序退出
```

#### 输入密码
```
>>> import getpass
>>> user = getpass.getuser()
>>> passwd = getpass.getpass()
Password: 
```

#### 获取终端大小 
```
import os
sz = os.get_terminal_size() 
```
#### 复制文件
```
Import shutil
shutil.copy(src , dst)
shutil.copy2(src , dst)
shutil.copytree(src , dst)
shutil.move(src , dst)
```

#### 文件归档
```py
import shuti
>>> shutil.make_archive('oop' , 'zip' , './oop')    #创建压缩文件
'/Users/zeopean/Sites/pycode/oop.zip'
>>> shutil.unpack_archive('oop.zip')                #解压
>>> os.system('ls')                                 #实现系统shell
>>> shutil.get_archive_formats()                    #查看压缩格式
[('bztar', "bzip2'ed tar-file"), ('gztar', "gzip'ed tar-file"), ('tar', 'uncompressed tar file'), ('xztar', "xz'ed tar-file"), ('zip', 'ZIP file')]
>>> 
```

#### webbrowser  浏览器模块
```
import webbrowser
webbrowser.open("http://www.zeopean.com")       #打开页面
webbrowser.open_new("http://www.baidu.com")
webbrowser.open_new_tab("http://php.net")
```



