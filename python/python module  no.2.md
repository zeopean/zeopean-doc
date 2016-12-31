
Python 模块

### apply 模块

- 基本用法

```
def function(a , b):
	print a , b

apply(function , ('hello' , 'world'))
apply(function , (1, 2+3))
apply(function , ('hello apply',) , {"b":"ok"})
apply(function , () , {"a":'hllo0' , "b":23})
```


### 实现子类基础基类的构造方法

```
#encoding=utf-8
#基类
class Rectangle:
	def __init__(self , color="red" , width=10 , height=19):
		print "create a ",color,self,"seized:",width,"x",height

#子类
class RoundedRectangle(Rectangle):
	def __init__(self ,**kw):
		apply(Rectangle.__init__ , (self,) , kw)

#实例化对象
# 基类对象
rect = Rectangle(color="green" , height=100 ,width=108)

# 子类对象


Rrect = RoundedRectangle(color='blue' , height=140)
```

### __import__ 模块

### 函数加载模块

```
#encoding=utf-8
import glob , os
modules = []

for module_file in glob.glob("*-plugin.py"):
	try:
		module_name , ext = os.path.splitext(os.path.basename(module_file))
		module = __import__(module_name)
		modules.append(module)
	except ImportError:
		pass

for module in modules:
	module.hello()
```

### 延迟加载模块

```
#encoding=utf-8
class LazyImport:
	def __init__(self , module_name):
		self.module_name = module_name
		self.module = None

	def __getattr__(self , name):
		if self.module is None:
			self.module = __import__(self.module_name)
		return getattr(self.module , name)

string = LazyImport("string")

print string.lowercase

```


### dir 模块

```
#encoding=utf-8
def dump(value):
	print value , '=>' , dir(value)

import sys

dump(0)

dump(1.0)

dump(0.0j)

dump([])

dump({})

dump("string")

dump(len)

dump(sys)
```

- dir获取类成员属性

```
#encoding=utf-8
class A:
	def a(self):
		pass
	def b(self):
		pass

class B(A):
	def c(self):
		pass
	def d(self):
		pass

#获取类成员属性
def getMembers(kclass , members=None):
	if members is None:
		members = []

	for k in kclass.__bases__:
		getMembers(k , members)

	for m in dir(kclass):
		if m not in members:
			members.append(m)

	return members

print getMembers(A)
print getMembers(B)
print getMembers(IOError)

vars 模块
book = 'book'
pages = 10
scripts = 300

print "The %(book)s book contains more than %(scripts)s scripts" % vars()

```

### callable 模块

```
#encoding=utf-8
#使用callable 函数
def dump(function):
	if callable(function):
		print function , "is callable"
	else:
		print function , "is not callable"

class A:
	def method(self , value):
			return value
class B(A):
	def __call__(self , value):
		return value

a = A()
b = B()

dump(0)

dump("string")

dump(callable)

dump(dump)

dump(A)
dump(A.method)

dump(B.method)

```


### eval 模块

```
 	print eval("__import__('os').getcwd()")
```

### compile 模块

compile(str ,filename ,kind )函数将一个字符串编译为字节代码, str是将要被编译的字符串, filename是定义该字符串变量的文件，kind参数指定了代码被编译的类型-- 'single'指单个语句, 'exec'指多个语句, 'eval'指一个表达式. cmpile()函数返回一个代码对象，该对象当然也可以被传递给eval_r()函数和exec语句来执行,例如:

```
>>> str = 'for i in range(0, 10): print i'
>>> c = compile(str,'','exec')      # 编译为字节代码对象 
>>> exec c      
```

### os 模块  	

#### os模块概述
Python os模块包含普遍的操作系统功能。如果你希望你的程序能够与平台无关的话，这个模块是尤为重要的。(一语中的)

#### 常用方法

1. os.name
输出字符串指示正在使用的平台。如果是window 则用'nt'表示，对于Linux/Unix用户，它是'posix'。

2. os.getcwd()
函数得到当前工作目录，即当前Python脚本工作的目录路径。

3. os.listdir()
返回指定目录下的所有文件和目录名。

```
>>> os.listdir(os.getcwd())
['Django', 'DLLs', 'Doc', 'include', 'Lib', 'libs', 'LICENSE.txt', 'MySQL-python-wininst.log', 'NEWS.txt', 'PIL-wininst.log', 'python.exe', 'pythonw.exe', 'README.txt', 'RemoveMySQL-python.exe', 'RemovePIL.exe', 'Removesetuptools.exe', 'Scripts', 'setuptools-wininst.log', 'tcl', 'Tools', 'w9xpopen.exe']>>> 
```

4. os.remove()
删除一个文件。

5. os.system()
运行shell命令。

```
>>> os.system('dir')
0>>> os.system('cmd') #启动dos
```

6. os.sep 可以取代操作系统特定的路径分割符。
7. os.linesep字符串给出当前平台使用的行终止符

```
>>> os.linesep'\r\n'        #Windows使用'\r\n'，Linux使用'\n'而Mac使用'\r'。
>>> os.sep'\\'              #Windows
>>> 
```

8. os.path.split() 函数返回一个路径的目录名和文件名

```
>>> os.path.split('C:\\Python25\\abc.txt')
('C:\\Python25', 'abc.txt')
```

9. os.path.isfile()和os.path.isdir() 函数分别检验给出的路径是一个文件还是目录。

```
>>> os.path.isdir(os.getcwd())
True>>> os.path.isfile('a.txt')
False
```

10. os.path.exists() 函数用来检验给出的路径是否真地存在

```
>>> os.path.exists('C:\\Python25\\abc.txt')
False>>> os.path.exists('C:\\Python25')
True>>>
```
 
11. os.path.abspath(name):		获得绝对路径
12. os.path.normpath(path):	规范path字符串形式
13. os.path.getsize(name):		获得文件大小，如果name是目录返回0L
14. os.path.splitext():			分离文件名与扩展名
```
>>> os.path.splitext('a.txt')
('a', '.txt')
```

15. os.path.join(path,name):	连接目录与文件名或目录

```
	>>> os.path.join('c:\\Python','a.txt')'c:\\Python\\a.txt'
	>>> os.path.join('c:\\Python','f1')'c:\\Python\\f1'
	>>> 
```

16. os.path.basename(path):	返回文件名

```	
	>>> os.path.basename('a.txt')'a.txt'
	>>> os.path.basename('c:\\Python\\a.txt')'a.txt'
	>>> 
```

17.os.path.dirname(path):		返回文件路径

```
>>> os.path.dirname('c:\\Python\\a.txt')'c:\\Python'
```

#### os.stat 模块

- 当我们使用os.stat(path)获取一个文件(夹)信息的时候， os.stat(path)本身返回的是一个元组如：      nt.stat_result(st_mode=33206, st_ino=203224933185146561, st_dev=0,st_nlink=1, st_uid=0, st_gid=0, st_size=21090, st_atime=1376373336,st_mtime=1376534141, st_ctime=1376373336)

- 在这个元组中，包含了10个属性：

```
    st_mode -- protection bits(模式)     st_ino -- inode number(索引号)     st_dev -- device(设备)     st_nlink -- number of hard links(硬链接号)     st_uid -- user id of owner(用户id)     st_gid -- group id of owner (组id)     st_size -- size of file,in bytes (大小)     st_atime -- time of most recent access expressed in seconds (访问时间)     st_mtime -- time of most recent content modificatin expressed in seconds (修改时间)     st_ctime -- platform dependent;time of most recent metadata change on Unix,or the teime of creation on Windows,expressed in senconds (根据不同操作系统而定)
```

#### os.time 模块

	在开始之前，首先要说明这几点：（转）
	在Python中，通常有这几种方式来表示时间：1）时间戳 2）格式化的时间字符串 3）元组（struct_time）共九个元素。由于Python的time模块实现主要调用C库，所以各个平台可能有所不同。
	UTC（Coordinated Universal Time，世界协调时）亦即格林威治天文时间，世界标准时间。在中国为UTC+8。DST（Daylight Saving Time）即夏令时。
	时间戳（timestamp）的方式：通常来说，时间戳表示的是从1970年1月1日00:00:00开始按秒计算的偏移量。我们运行“type(time.time())”，返回的是float类型。返回时间戳方式的函数主要有time()，clock()等。
	元组（struct_time）方式：struct_time元组共有9个元素，返回struct_time的函数主要有gmtime()，localtime()，strptime()。下面列出这种方式元组中的几个元素：








### time模块中常用的几个函数：

1）time.localtime([secs])：将一个时间戳转换为当前时区的struct_time。secs参数未提供，则以当前时间为准。

```
>>> time.localtime() time.struct_time(tm_year=2011, tm_mon=5, tm_mday=5, tm_hour=14, tm_min=14, tm_sec=50, tm_wday=3, tm_yday=125, tm_isdst=0) >>> time.localtime(1304575584.1361799) time.struct_time(tm_year=2011, tm_mon=5, tm_mday=5, tm_hour=14, tm_min=6, tm_sec=24, tm_wday=3, tm_yday=125, tm_isdst=0)

```

2）time.gmtime([secs])：和localtime()方法类似，gmtime()方法是将一个时间戳转换为UTC时区（0时区）的struct_time。

```
>>>time.gmtime() time.struct_time(tm_year=2011, tm_mon=5, tm_mday=5, tm_hour=6, tm_min=19, tm_sec=48, tm_wday=3, tm_yday=125, tm_isdst=0)

```

3）time.time()：返回当前时间的时间戳。

```
>>> time.time()  1304575584.1361799

```

4）time.mktime(t)：将一个struct_time转化为时间戳。

```
>>> time.mktime(time.localtime()) 1304576839.0

```

5）time.sleep(secs)：线程推迟指定的时间运行。单位为秒。

6）time.clock()：这个需要注意，在不同的系统上含义不同。在UNIX系统上，它返回的是“进程时间”，它是用秒表示的浮点数（时间戳）。而在WINDOWS中，第一次调用，返回的是进程运行的实际时间。而第二次之后的调用是自第一次调用以后到现在的运行时间。（实际上是以WIN32上QueryPerformanceCounter()为基础，它比毫秒表示更为精确）

```
运行结果：
clock1:3.35238137808e-006  clock2:1.00004944763  clock3:2.00012040636
其中第一个clock()输出的是程序运行时间 第二、三个clock()输出的都是与第一个clock的时间间隔

```

7）time.asctime([t])：把一个表示时间的元组或者struct_time表示为这种形式：'Sun Jun 20 23:21:05 1993'。如果没有参数，将会将time.localtime()作为参数传入。

```
>>> time.asctime() 'Thu May 5 14:55:43 2011'

```

8）time.ctime([secs])：把一个时间戳（按秒计算的浮点数）转化为time.asctime()的形式。如果参数未给或者为None的时候，将会默认time.time()为参数。它的作用相当于
time.asctime(time.localtime(secs))。

```

>>> time.ctime() 'Thu May 5 14:58:09 2011' >>> time.ctime(time.time()) 'Thu May 5 14:58:39 2011' >>> time.ctime(1304579615) 'Thu May 5 15:13:35 2011'

```

time.strftime(format[, t])：把一个代表时间的元组或者struct_time（如由

time.localtime()和time.gmtime()返回）转化为格式化的时间字符串。如果t未指定，将传入time.localtime()。如果元组中任何一个元素越界，ValueError的错误将会被抛出。

##### python中时间日期格式化符号： 
```
%y 两位数的年份表示（00-99） %Y 四位数的年份表示（000-9999） %m 月份（01-12） %d 月内中的一天（0-31） %H 24小时制小时数（0-23） %I 12小时制小时数（01-12）  %M 分钟数（00=59） %S 秒（00-59）  %a 本地简化星期名称 %A 本地完整星期名称 %b 本地简化的月份名称 %B 本地完整的月份名称 %c 本地相应的日期表示和时间表示 %j 年内的一天（001-366） %p 本地A.M.或P.M.的等价符 %U 一年中的星期数（00-53）星期天为星期的开始 %w 星期（0-6），星期天为星期的开始 %W 一年中的星期数（00-53）星期一为星期的开始 %x 本地相应的日期表示 %X 本地相应的时间表示 %Z 当前时区的名称 %% %号本身  

```


### math 模块

math.fabs(-1.1)    	#绝对值
math.ceil(i)  		#这个方法对i向上取整，i = 1.3 ，返回值为2 math.floor(i)  		#正好与上面相反，是向下取整。i = 1.4，返回1 math.pow(a, b)  		#返回a的b次方 math.sqrt(i)  		#返回i的平方根


### copy 模块

```
#encoding=utf-8
import copy
lst = [1,23,4,4]
lst_c = copy.copy(lst)

#copy
print 'lst:=>',lst
print 'lst_c:=>',lst_c

#对lst_c 进行追加
lst.append(['a','b'])
print '\r\n--------------append after-------------'
print 'lst:=>',lst
print 'lst_c:=>',lst_c

#进行深度deepcopy
lst_dcopy = copy.deepcopy(lst)
print '\r\n--------------deepcopy after----------'
print 'lst:=>',lst
print 'lst_dcopy:=>',lst_dcopy

print '\r\n------------deepcopy append after-------'
lst_dcopy.append(['e','r'])
print 'lst:=>',lst
print 'lst_dcopy:=>',lst_dcopy

```

### sys 模块

1) sys.stdin 标准输入流。
2) sys.stdout 标准输出流。
3) sys.stderr 标准错误流。
4) sys.path 查找模块所在目录的目录名列表。
5) sys.argv 命令行的参数，包括脚本名称。
6) sys.platform 返回当前系统平台，如：win32、Linux等。

### gc 模块

```
#encoding=utf-8

#使用python gc 模块进行垃圾回收
import gc

class Node:
	def __init__(self , name):
		self.name 	= name 
		self.parent = None
		self.children 	= []

	def addchild(self , node):
		node.parent = self
		self.children.append(node)\

def __repr__(self):
	return '<node %s at %x>' % (repr(self.name) , id(self))

root = Node('monty')

root.addchild(Node('eric'))
root.addchild(Node('john'))
root.addchild(Node('michael'))

del root

print gc.collect() , 'unreachable objects'
print gc.collect() , 'unreachable objects'

```

### operator模块 

```
#encoding=utf-8
import operator
import UserList

sequence = 1 ,2 ,4
#加
print "add: => ", reduce(operator.add , sequence) 
#减
print "sub: => ", reduce(operator.sub , sequence) 
#乘
print "mul: => ", reduce(operator.mul , sequence) 
#字符串拼接
print "concat: => ", operator.concat('zeopean ' , 'daming')
#字符串重复
print "repeat:=>", operator.repeat('zeopean ',3)
#按键值获取元素
print "getitem:=>", operator.getitem(sequence,2)
#获取元素坐标
print "indexOf:=>", operator.indexOf(sequence , 4)
#判断元素是否在sequence中
print "sequenceIncludes:=>",operator.sequenceIncludes(sequence,2)

def dump(data):
	print type(data),':=>', 
	if operator.isCallable(data):
		print 'CALLABLE',
	if operator.isMappingType(data):
		print "MAPPING",
	if operator.isNumberType(data):
		print "Number"
	if operator.isSequenceType(data):
		print "Sequence",
	print 

print '>--------------->--------------->'
dump(0)					#整数
dump('string')				#字符串
dump([1,24,4,5])			#数组
dump((1,2,3))				#元组
dump({"a":1})				#字典
dump(len)					#函数
dump(UserList)				#模块
dump(UserList.UserList)		#类
dump(UserList.UserList()) 	#类对象

```


### string 模块

- 常见方法

```
>>> string.ascii_letters		#ascii 字符
'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'

>>> string.ascii_lowercase	#ascii 小写字符
'abcdefghijklmnopqrstuvwxyz'

>>> string.ascii_uppercase 	#ascii 大写字符
'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

>>> string.digits 				#十进制字符
'0123456789'

>>> string.hexdigits 			#十六进制字符
'0123456789abcdefABCDEF'

>>> string.letters				#字母字符
'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'

>>> string.lowercase			#小写字母
'abcdefghijklmnopqrstuvwxyz'

>>> string.uppercase			#大写字符
'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

>>> string.octdigits			#十六进制字符
'01234567'

>>> string.punctuation			#特殊字符
'!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'

>>> string.printable			#所有英文字符
'0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'

>>> string.whitespace			#不可见字符
'\t\n\x0b\x0c\r

```


### 字符串详细操作
可以将这些方法按功能用途划分为以下几种类型：

#### 字符串格式输出对齐

```
>>> str='stRINg lEArn'
>>>
>>> str.center(20)      #生成20个字符长度，str排中间
'    stRINg lEArn    '
>>> 
>>> str.ljust(20)       #str左对齐
'stRINg lEArn        '  
>>>
>>> str.rjust(20)       #str右对齐
'        stRINg lEArn'
>>> 
>>> str.zfill(20)       #str右对齐，左边填充0
'00000000stRINg lEArn'
大小写转换
>>> str='stRINg lEArn' 
>>> 
>>> str.upper() #转大写
'STRING LEARN'
>>> 
>>> str.lower() #转小写
'string learn'
>>> 
>>> str.capitalize() #字符串首为大写，其余小写
'String learn'
>>> 
>>> str.swapcase() #大小写对换
'STrinG LeaRN'
>>> 
>>> str.title() #以分隔符为标记，首字符为大写，其余为小写
'String Learn'

```

#### 字符串条件判断

```
>>> str='0123'
>>> str.isalnum()  #是否全是字母和数字，并至少有一个字符 
True
>>> str.isdigit()   #是否全是数字，并至少有一个字符
True

>>> str='abcd'
>>> str.isalnum()
True
>>> str.isalpha()   #是否全是字母，并至少有一个字符
True
>>> str.islower()   #是否全是小写，当全是小写和数字一起时候，也判断为True 
True

>>> str='abcd0123'
>>> str.islower()   #同上
True
>>> str.isalnum()   
True

>>> str=' '
>>> str.isspace()    #是否全是空白字符，并至少有一个字符
True
>>> str='ABC'
>>> str.isupper()    #是否全是大写，当全是大写和数字一起时候，也判断为True
True
>>> str='Abb Acc'
>>> str.istitle()    #所有单词字首都是大写，标题
True

>>> str='string learn'
>>> str.startswith('str') #判断字符串以'str'开头
True
>>> str.endswith('arn')   #判读字符串以'arn'结尾
True

```

#### 字符串搜索定位与替换

```
>>> str='string lEARn'
>>> 
>>> str.find('a')      #查找字符串，没有则返回-1，有则返回查到到第一个匹配的索引
-1
>>> str.find('n')
4
>>> str.rfind('n')     #同上，只是返回的索引是最后一次匹配的
11
>>> 
>>> str.index('a')     #如果没有匹配则报错
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: substring not found
>>> str.index('n')     #同find类似,返回第一次匹配的索引值
4
>>> str.rindex('n')    #返回最后一次匹配的索引值
11
>>>
>>> str.count('a')     #字符串中匹配的次数
0
>>> str.count('n')     #同上
2
>>>
>>> str.replace('EAR','ear')  #匹配替换
'string learn'
>>> str.replace('n','N')
'striNg lEARN'
>>> str.replace('n','N',1)
'striNg lEARn'
>>>
>>>
>>> str.strip('n')   #删除字符串首尾匹配的字符，通常用于默认删除回车符
'string lEAR'
>>> str.lstrip('n')  #左匹配
'string lEARn'
>>> str.rstrip('n')  #右匹配
'string lEAR'
>>>
>>> str=' tab'
>>> str.expandtabs()  #把制表符转为空格
'      tab'
>>> str.expandtabs(2) #指定空格数
' tab'

```

#### 字符串编码与解码

```
>>> str='字符串学习'
>>> str
'\xe5\xad\x97\xe7\xac\xa6\xe4\xb8\xb2\xe5\xad\xa6\xe4\xb9\xa0'
>>> 
>>> str.decode('utf-8')               #解码过程，将utf-8解码为unicode
u'\u5b57\u7b26\u4e32\u5b66\u4e60'

>>> str.decode('utf-8').encode('gbk')  #编码过程，将unicode编码为gbk
'\xd7\xd6\xb7\xfb\xb4\xae\xd1\xa7\xcf\xb0'
>>> str.decode('utf-8').encode('utf-8')  #将unicode编码为utf-8
'\xe5\xad\x97\xe7\xac\xa6\xe4\xb8\xb2\xe5\xad\xa6\xe4\xb9\xa0'

```

#### 字符串分割变换

```
>>> str='Learn string'
>>> '-'.join(str)
'L-e-a-r-n- -s-t-r-i-n-g'
>>> l1=['Learn','string']
>>> '-'.join(l1)
'Learn-string'
>>> 
>>> str.split('n')
['Lear', ' stri', 'g']
>>> str.split('n',1)
['Lear', ' string']
>>> str.rsplit('n',1)
['Learn stri', 'g']
>>>
>>> str.splitlines()
['Learn string']
>>>
>>> str.partition('n')
('Lear', 'n', ' string')
>>> str.rpartition('n')
('Learn stri', 'n', 'g')

```


### re模块 

Python通过re模块提供对正则表达式的支持。使用re的一般步骤是先将正则表达式的字符串形式编译为Pattern实例，然后使用Pattern实例处理文本并获得匹配结果（一个Match实例），最后使用Match实例获得信息，进行其他的操作。

```
re.compile(strPattern[, flag]):
这个方法是Pattern类的工厂方法，用于将字符串形式的正则表达式编译为Pattern对象。 第二个参数flag是匹配模式，取值可以使用按位或运算符'|'表示同时生效，比如re.I | re.M。另外，你也可以在regex字符串中指定模式，比如re.compile('pattern', re.I | re.M)与re.compile('(?im)pattern')是等价的。  可选值有：
re.I(re.IGNORECASE): 忽略大小写（括号内是完整写法，下同）
M(MULTILINE): 多行模式，改变'^'和'$'的行为（参见上图）
S(DOTALL): 点任意匹配模式，改变'.'的行为
L(LOCALE): 使预定字符类 \w \W \b \B \s \S 取决于当前区域设定
U(UNICODE): 使预定字符类 \w \W \b \B \s \S \d \D 取决于unicode定义的字符属性
X(VERBOSE): 详细模式。这个模式下正则表达式可以是多行，忽略空白字符，并可以加入注释。以下两个正则表达式是等价的：

re提供了众多模块方法用于完成正则表达式的功能。这些方法可以使用Pattern实例的相应方法替代，唯一的好处是少写一行re.compile()代码，但同时也无法复用编译后的Pattern对象。这些方法将在Pattern类的实例方法部分一起介绍。如上面这个例子可以简写为：

re模块还提供了一个方法escape(string)，用于将string中的正则表达式元字符如*/+/?等之前加上转义符再返回，在需要大量匹配元字符时有那么一点用。
Match
Match对象是一次匹配的结果，包含了很多关于此次匹配的信息，可以使用Match提供的可读属性或方法来获取这些信息。
属性：
string: 匹配时使用的文本。
re: 匹配时使用的Pattern对象。
pos: 文本中正则表达式开始搜索的索引。值与Pattern.match()和Pattern.seach()方法的同名参数相同。
endpos: 文本中正则表达式结束搜索的索引。值与Pattern.match()和Pattern.seach()方法的同名参数相同。
lastindex: 最后一个被捕获的分组在文本中的索引。如果没有被捕获的分组，将为None。
lastgroup: 最后一个被捕获的分组的别名。如果这个分组没有别名或者没有被捕获的分组，将为None。
方法：
group([group1, …]):  获得一个或多个分组截获的字符串；指定多个参数时将以元组形式返回。group1可以使用编号也可以使用别名；编号0代表整个匹配的子串；不填写参数时，返回group(0)；没有截获字符串的组返回None；截获了多次的组返回最后一次截获的子串。
groups([default]):  以元组形式返回全部分组截获的字符串。相当于调用group(1,2,…last)。default表示没有截获字符串的组以这个值替代，默认为None。
groupdict([default]):  返回以有别名的组的别名为键、以该组截获的子串为值的字典，没有别名的组不包含在内。default含义同上。
start([group]):  返回指定的组截获的子串在string中的起始索引（子串第一个字符的索引）。group默认值为0。
end([group]):  返回指定的组截获的子串在string中的结束索引（子串最后一个字符的索引+1）。group默认值为0。
span([group]):  返回(start(group), end(group))。
expand(template):  将匹配到的分组代入template中然后返回。template中可以使用\id或\g<id>、\g<name>引用分组，但不能使用编号0。\id与\g<id>是等价的；但\10将被认为是第10个分组，如果你想表达\1之后是字符'0'，只能使用\g<1>0。

 Pattern
Pattern对象是一个编译好的正则表达式，通过Pattern提供的一系列方法可以对文本进行匹配查找。
Pattern不能直接实例化，必须使用re.compile()进行构造。
Pattern提供了几个可读属性用于获取表达式的相关信息：
pattern: 编译时用的表达式字符串。
flags: 编译时用的匹配模式。数字形式。
groups: 表达式中分组的数量。
groupindex: 以表达式中有别名的组的别名为键、以该组对应的编号为值的字典，没有别名的组不包含在内。

实例方法[ | re模块方法]：
match(string[, pos[, endpos]]) | re.match(pattern, string[, flags]):  这个方法将从string的pos下标处起尝试匹配pattern；如果pattern结束时仍可匹配，则返回一个Match对象；如果匹配过程中pattern无法匹配，或者匹配未结束就已到达endpos，则返回None。  pos和endpos的默认值分别为0和len(string)；re.match()无法指定这两个参数，参数flags用于编译pattern时指定匹配模式。  注意：这个方法并不是完全匹配。当pattern结束时若string还有剩余字符，仍然视为成功。想要完全匹配，可以在表达式末尾加上边界匹配符'$'。  示例参见2.1小节。
search(string[, pos[, endpos]]) | re.search(pattern, string[, flags]):  这个方法用于查找字符串中可以匹配成功的子串。从string的pos下标处起尝试匹配pattern，如果pattern结束时仍可匹配，则返回一个Match对象；若无法匹配，则将pos加1后重新尝试匹配；直到pos=endpos时仍无法匹配则返回None。  pos和endpos的默认值分别为0和len(string))；re.search()无法指定这两个参数，参数flags用于编译pattern时指定匹配模式。 


split(string[, maxsplit]) | re.split(pattern, string[, maxsplit]):  按照能够匹配的子串将string分割后返回列表。maxsplit用于指定最大分割次数，不指定将全部分割。 


findall(string[, pos[, endpos]]) | re.findall(pattern, string[, flags]):  搜索string，以列表形式返回全部能匹配的子串。 


finditer(string[, pos[, endpos]]) | re.finditer(pattern, string[, flags]):  搜索string，返回一个顺序访问每一个匹配结果（Match对象）的迭代器。 


sub(repl, string[, count]) | re.sub(pattern, repl, string[, count]):  使用repl替换string中每一个匹配的子串后返回替换后的字符串。  当repl是一个字符串时，可以使用\id或\g<id>、\g<name>引用分组，但不能使用编号0。  当repl是一个方法时，这个方法应当只接受一个参数（Match对象），并返回一个字符串用于替换（返回的字符串中不能再引用分组）。  count用于指定最多替换次数，不指定时全部替换。 


subn(repl, string[, count]) |re.sub(pattern, repl, string[, count]):  返回 (sub(repl, string[, count]), 替换次数)。 

```

