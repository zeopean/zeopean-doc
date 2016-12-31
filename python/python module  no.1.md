

#### json -- dumps/loads
```
#encoding=utf-8

#使用json 模块
import json

I = ['daming' ,[1,2,3] , {'key':1}]

#进行 json 编码
print 'encode_json--->'
print repr(I)
print json.dumps(I)

#进行json 解码
print 'decode_json--->'
jsonStr = json.dumps(I)
print jsonStr
print json.loads(jsonStr)
```


#### thread/threading -- 多线程
1) 模块的Thread函数的可以实例化一个对象，每个Thread对象对应一个线程，可以通过start()方法，运行线程。
2) threading.activeCount()方法返回当前”进程”里面”线程”的个数，注：返回的个数中包含主线程。类似python统计列表中元素个数。
3) threading.enumerate()的方法，返回当前运行中的Thread对象列表。
4) threading.setDaemon()方法，参数设置为True的话会将线程声明为守护线程，必须在start() 方法之前设置，不设置为守护线程程序会被无限挂起。

```
Demo1
#encoding=utf-8

#多线程的使用 
import threading
import time 

def thread_main(a):
	global count , mutex 
	#获取线程名字
	threadname = threading.currentThread().getName()

	#进行循环操作
	for x in xrange(0 , int(a)):
		#加锁
		mutex.acquire();
		count = count + 1
		#解锁
		mutex.release()
		#输出进程名，计数器
		print threadname , x , count

		time.sleep(1)

def main(num):
	global count , mutex
	threads = []
	count 	= 1
	#创建锁
	mutex 	= threading.Lock()

	for x in xrange(0 , num):
		threads.append(threading.Thread(target=thread_main , args=(10,)))

	#开启所有进程
	for t in threads:
		t.start()

	#主进程等待退出
	for t in threads:
		t.join()

if __name__ == '__main__':
	num = 4
	main(4)
```

```
Demo2
#encoding=utf-8

#使用threading.thread  类方法

import threading 
import time 

class Test(threading.Thread):
	#初始化
	def __init__(self , num):
		threading.Thread.__init__(self)
		self._run_num = num

	def run(self):
		global count , mutex
		threadname = threading.currentThread().getName()

		for x in xrange(0 , int(self._run_num)):
			#加锁
			mutex.acquire()
			count = count + 1
			#解锁
			mutex.release()
			print threadname , x, count
			time.sleep(1)

if __name__ == '__main__':
	global count , mutex
	threads = [] 
	num 	= 4
	count  	= 1

	#加锁
	mutex = threading.Lock()

	for x in xrange(0 , num):
		#添加线程对象
		threads.append(Test(10))

	#启动线程
	for t in threads:
		t.start()

	#等待进程结束
	for t in threads:
		t.join()
```


#### Sqlite3 -- 微型数据库
1 )、commit() ，事务提交
2 )、rollback() ，事务回滚
3 )、cursor() ，创建游标
4 )、close() ， 关闭一个连接
在创建了游标之后，它有以下可以操作的方法
```
import sqlite3
cur = db.cursor()
cur.execute(“sql语句”)
cur....

execute()，执行sql语句
scroll()，游标滚动
close()，关闭游标
executemany，执行多条sql语句 
fetchone()，从结果中取一条记录
fetchmany()，从结果中取多条记录
fetchall()，从结果中取出多条记录
```

#### urllib 模块
```
>>> import urllib
#urlopen 打开url
>>> baidu = urllib.urlopen(‘http://www.baidu.com/’)
>>> print baidu.info 			#输出baidu首页头部信息
>>> print baidu.getcode() 		#输出baidu首页网页的状态码
>>> print baidu.geturl() 		#输出请求的url地址
>>> for line in baidu:
>>>     print line,
>>> baidu.close() #关闭对象方法
```

#### cPickle && pickle 序列化
```
#encoding=utf-8

#使用 cPickle 以及 pickle模块，实现数据持久化存储

try:
	import cPickle as pickle
except:
	import pickle
import pprint 

info = [1,2,4,5,'ab','cd',['demo',11],(3,45,'33')]
print "原始数据：->"
pprint.pprint(info)

data1 = pickle.dumps(info)
data2 = pickle.loads(data1)

print '序列化：%r' % data1
print '反序列化： %r' % data2
```


#### 快速读取文件 linecache
```
#encoding=utf-8
#使用 linecache 读取文件

import os
import linecache

def get_content(path):
	#读取缓存文件内容
	if os.path.exists(path):
		content = '' 
		cache_data = linecache.getlines(path,1)
		for line in range(len(cache_data)):
			content += cache_data[line]
		return content
	else:
		print "the path [{}] is not exists!".format()

if __name__ == '__main__':
	path = 'E:/error.log'
	content = get_content(path)
	print content
```

#### cookielib 的使用
```
#encoding=utf-8
import Cookie 
import cookielib
import urllib
import urllib2 

#cookie 的使用
c  = cookielib.LWPCookieJar()	#获取cookie
opener = urllib2.build_opener(urllib2.HTTPCookieProcessor(c))
login_path = "http://www.zeopean.com/index.php?s=/Home/User/login.html"

data = {'username':'zeopean','password':'zeopean','verify':'vrcc2'}
post_info = urllib.urlencode(data)
request = urllib2.Request(login_path , post_info)
html = opener.open(request).read()

if c:
	print c 
c.save('cookie.txt')
```


#### random  获取随机数

    random.random()函数是这个模块中最常用的方法了，它会生成一个随机的浮点数，范围是在0.0~1.0之间。
    random.uniform()正好弥补了上面函数的不足，它可以设定浮点数的范围，一个是上限，一个是下限。
    random.randint()随机生一个整数int类型，可以指定这个整数的范围，同样有上限和下限值，python random.randint。
    random.choice()可以从任何序列，比如list列表中，选取一个随机的元素返回，可以用于字符串、列表、元组等。
    random.shuffle()如果你想将一个序列中的元素，随机打乱的话可以用这个函数方法。
    random.sample()可以从指定的序列中，随机的截取指定长度的片断，不作原地修改。

#### base64 base64编码

```
import  base64
#编码
encode = base64.b64encode(‘文本字符串’)

#解码
decode = base64.b64decode(encode)
```


#### urlparse url返回元组

    1. urlparse.urlparse(url)，分解url返回元组，可以得到很多关于这个url的数据，网络协议、目录层次等。
    
    2. urlparse.urlunparse(parts)，它接收一个元组类型，将元组内对应元素重新组后为一个url网址，与上面功能正好相反。
    
    3. urlparse.urlsplit(url)，作用与urlparse非常相似，它不会分解url参数，对于遵循RFC2396的URL很有用处。
    
    4. urlparse.urljoin(base, url ) 功能是基于一个base url和另一个url构造一个绝对URL。



#### heapq
-- nlargest  		最大值 
-- nsmallest  	最小值
-- heapify 		首个元素最前
-- heappop 		弹出最小元素
-- heappush 		插入元素

--
```
import heapq
nums = [1, 8, 2, 23, 7, -4, 18, 23, 42, 37, 2]
print(heapq.nlargest(3, nums)) # Prints [42, 37, 23]
print(heapq.nsmallest(3, nums)) # Prints [-4, 1, 2]
```
-- 
```
portfolio = [
{'name': 'IBM', 'shares': 100, 'price': 91.1},
{'name': 'AAPL', 'shares': 50, 'price': 543.22},
{'name': 'FB', 'shares': 200, 'price': 21.09},
{'name': 'HPQ', 'shares': 35, 'price': 31.75},
{'name': 'YHOO', 'shares': 45, 'price': 16.35},
{'name': 'ACME', 'shares': 75, 'price': 115.65}
]
cheap = heapq.nsmallest(3, portfolio, key=lambda s: s['price'])
expensive = heapq.nlargest(3, portfolio, key=lambda s: s['price'])
```

--
```
nums = [1, 8, 2, 23, 7, -4, 18, 23, 42, 37, 2]
import heapq
heapq.heapify(nums)

heapq.heappop(nums)
heapq.heappush(nums)
```


#### collections 
- defaultdict
```
from collections import defaultdict

d = defaultdict(list)
d['a'].append(1)
d['a'].append(2)
d['b'].append(4)

d = defaultdict(set)
d['a'].add(1)
d['a'].add(2)
d['b'].add(4)
```


- deque
```
from collections import deque

def search(lines, pattern, history=5):
previous_lines = deque(maxlen=history)
for li in lines:
if pattern in li:
yield li, previous_lines
previous_lines.append(li)

#Example use on a file
if __name__ == '__main__':
with open(r'../../cookbook/somefile.txt') as f:
for line, prevlines in search(f, 'python', 5):
for pline in prevlines:
print(pline, end='')
print(line, end='')
print('-' * 20)

```
- OrderedDict  
 ```
>>> from collections import OrderedDict
>>> import json
>>> d = OrderedDict()   -- 有序字典
>>> d['foo']  = 1
>>> d['bar']  = 2
>>> d['span'] = 3
>>> d['grok'] = 4
>>>
>>> for key in d:
...     print(key , d[key])
...
foo 1
bar 2
span 3
grok 4
>>> json.dumps(d)			-- json 格式
'{"foo": 1, "bar": 2, "span": 3, "grok": 4}'
```

- 字典的运算
```
prices = {
'ACME': 45.23,
'AAPL': 612.78,
'IBM': 205.55,
'HPQ': 37.20,
'FB': 10.75
}
    -- 最小值的获取
    >>> min_price = min(zip(prices.values() , prices.keys()))
    >>> min_price
    (10.75, 'FB')
    -- 最大值的获取
    >>> max_price = max(zip(prices.values() , prices.keys()))
    >>> max_price
    (612.78, 'AAPL')
    -- 字典排序
    >>> prices_sorted = sorted(zip(prices.values() , prices.keys()))
    >>> prices_sorted
    [(10.75, 'FB'), (37.2, 'HPQ'), (45.23, 'ACME'), (205.55, 'IBM'), (612.78, 'AAPL'
    )]
```
-- 不使用 zip ，使用lambda
min(prices, key=lambda k: prices[k]) # Returns 'FB'
max(prices, key=lambda k: prices[k]) # Returns 'AAPL'

min_value = prices[min(prices, key=lambda k: prices[k])]

-- 2个 字典对比
```
a = {
'x' : 1,
'y' : 2,
'z' : 3
}
b = {
'w' : 10,
'x' : 11,
'y' : 2
}

>>> a.keys() & b.keys()
{'y', 'x'}
>>> a.keys() - b.keys()
{'z'}
>>> a.items() & b.items()
{('y', 2)}
>>> c = {key:a[key] for key in a.keys() - {'z','w'}}
>>> c
{'y': 2, 'x': 1}

```

-- yield 配合字典使用
```
def dequpe(items):
	seen = set()
	for item in items :
		if item not in seen:
			yield item
			seen.add(item)

def dedupes(items , key=None):
	seen = set()
	for item in items :
		val = item if key is None else key(item)
		if val not in seen:
			yield item 
			seen.add(val)

if __name__ == '__main__':
	# a = [1,2323,23,23,23,23,21,312,23,22,2]
	# data = list(dequpe(a))
	# print(data)

	print('\r\n')
	b = [ {'x':1, 'y':2}, {'x':1, 'y':3}, {'x':1, 'y':2}, {'x':2, 'y':4}]
	print(list(dedupes(b, key=lambda d: (d['x'],d['y']))))
```


-- Counter 数据重复出现处理
```
words = [
'look', 'into', 'my', 'eyes', 'look', 'into', 'my', 'eyes',
'the', 'eyes', 'the', 'eyes', 'the', 'eyes', 'not', 'around', 'the',
'eyes', "don't", 'look', 'around', 'the', 'eyes', 'look', 'into',
'my', 'eyes', "you're", 'under'
]

>>> from collections import Counter
>>> word_counts = Counter(words)
>>> top_three = word_counts.most_common(3)
>>> top_three
[('eyes', 8), ('the', 5), ('look', 4)]

slice 
-- slice
>>> items = [0, 1, 2, 3, 4, 5, 6]
>>> a = slice(2, 4)
>>> items[2:4]
[2, 3]
>>> items[a]
[2, 3]
>>> items[a] = [10,11]
>>> items
[0, 1, 10, 11, 4, 5, 6]
>>> del items[a]
>>> items
[0, 1, 4, 5, 6]

>>> a = slice(5, 50, 2)
>>> a.start
5
>>> a.stop
50
>>> a.step
2
>>>
```

-- incides 
```
>>> s = 'HelloWorld'
>>> a.indices(len(s))
(5, 10, 2)
>>> for i in range(*a.indices(len(s))):
... print(s[i])
```


#### operator
```
rows = [
{'fname': 'Brian', 'lname': 'Jones', 'uid': 1003},
{'fname': 'David', 'lname': 'Beazley', 'uid': 1002},
{'fname': 'John', 'lname': 'Cleese', 'uid': 1001},
{'fname': 'Big', 'lname': 'Jones', 'uid': 1004}
]

from operator import itemgetter
-- 按fname 排序 
rows_by_fname = sorted(rows, key=itemgetter('fname'))
【-- 同rows_by_fname = sorted(rows, key=lambda r: r['fname'])】
-- 按uid 排序
rows_by_uid = sorted(rows, key=itemgetter('uid'))
【-- 同 rows_by_fname = sorted(rows, key=lambda r: r['uid'])】
print(rows_by_fname)
print(rows_by_uid)
```

#### itertools compress 
```
>>> addresses = [
... '5412 N CLARK',
... '5148 N CLARK',
... '5800 E 58TH',
... '2122 N CLARK'
... '5645 N RAVENSWOOD',
... '1060 W ADDISON',
... '4801 N BROADWAY' ]
>>> counts = [ 0, 3, 10, 4, 1, 7, 6, 1]
>>> from itertools import compress
>>> more5 = [n > 5 for n in counts]
>>> more5
[False, False, True, False, False, True, True, False]

>>> list(compress(addresses , more5))
['5800 E 58TH', '4801 N BROADWAY']
```


#### dict
-- dict 子集的处理
```
>>> prices = {
... 'ACME': 45.23,
... 'AAPL': 612.78,
... 'IBM': 205.55,
... 'HPQ': 37.20,
... 'FB': 10.75
... }
...
>>> p1 = {key:value for key ,value in prices.items() if value>200}
>>> tech_names = {'AAPL', 'IBM', 'HPQ', 'MSFT'}
>>> p2 = {key:value for key ,value in prices.items() if key in tech_names}
>>> p1
{'IBM': 205.55, 'AAPL': 612.78}
>>> p2
{'IBM': 205.55, 'AAPL': 612.78, 'HPQ': 37.2}
>>>


>>> p1 = dict((key,value) for key , value in prices.items() if value > 200)
>>> p1
{'IBM': 205.55, 'AAPL': 612.78}
>>> p2 = {key:prices[key] for key in prices.keys() & tech_names}
>>> p2
{'IBM': 205.55, 'AAPL': 612.78, 'HPQ': 37.2}
```

#### namedtuple
```
>>> from collections import namedtuple
>>> Subcriber = namedtuple("Subcriber" , ['addr','joind'])
>>> sub = Subcriber('zeop@qq.com' ,'2015-9')
>>> sub
Subcriber(addr='zeop@qq.com', joind='2015-9')
>>> sub.addr
'zeop@qq.com'
>>> sub.joind
'2015-9'
>>> addr , joind = sub
>>> addr
'zeop@qq.com'
>>> joind
'2015-9'


from collections import namedtuple
Stock = namedtuple('Stock', ['name', 'shares', 'price', 'date', 'time'])

stock_prototype = Stock('', 0, 0.0, None, None)

return stock_prototype._replace(**s)
```

#### 集聚方法
#文件名匹配
```
import os
files = os.listdir('.')		#判断本地文件
if any(name.endswith('.py') for name in files):
print('There be python!')
else:	
print('Sorry, no python.')
# 
s = ('ACME', 50, 123.45)
print(','.join(str(x) for x in s))

portfolio = [
{'name':'GOOG', 'shares': 50},
{'name':'YHOO', 'shares': 75},
{'name':'AOL', 'shares': 20},
{'name':'SCOX', 'shares': 65}
]
min_shares = min(s['shares'] for s in portfolio)
min_shares = min(portfolio, key=lambda s: s['shares'])
```


#### ChainMap 

```
#定义两个字典
a = {'x': 1, 'z': 3 }
b = {'y': 2, 'z': 4 }

from collections import ChainMap
c = ChainMap(a,b)
print(c['x']) # Outputs 1 (from a)
print(c['y']) # Outputs 2 (from b)
print(c['z']) # Outputs 3 (from a)
#打印输出
>>> len(c)
3
>>> list(c.keys())
['x', 'y', 'z']
>>> list(c.values())
[1, 2, 3]

>>> values = ChainMap()
>>> values['x'] = 1
 # Add a new mapping
>>> values = values.new_child()
>>> values['x'] = 2
     # Add a new mapping
>>> values = values.new_child()
>>> values['x'] = 3
>>> values
ChainMap({'x': 3}, {'x': 2}, {'x': 1})
>>> values['x']
3
    # Discard last mapping
>>> values = values.parents
>>> values['x']
2
     # Discard last mapping
>>> values = values.parents
>>> values['x']
1
>>> values
ChainMap({'x': 1})
```


#### re
#正则匹配

##### re.split
```
>>> line = 'asdf fjdk; afed, fjek,asdf, foo'
>>> import re
>>> re.split(r'[;,\s]\s*', line)
['asdf', 'fjdk', 'afed', 'fjek', 'asdf', 'foo']

>>> import re
>>> url = 'http://www.python.org'
>>> re.match('http:|https:|ftp:', url)
<_sre.SRE_Match object at 0x101253098>
```

##### re.match
```
>>> text1 = '11/27/2012'
>>> text2 = 'Nov 27, 2012'
>>>
>>> import re
>>> #Simple matching: \d+ means match one or more digits
>>> if re.match(r'\d+/\d+/\d+', text1):
... print('yes')
... else:
... print('no')
...
```

##### re.compile
 	datepat = re.compile(r'(\d+)/(\d+)/(\d+)')

##### re.findall 
```
>>> text = 'Today is 11/27/2012. PyCon starts 3/13/2013.'
>>> datepat.findall(text)
['11/27/2012', '3/13/2013']


Text = 'Today is 11/27/2012. PyCon starts 3/13/2013.'
>>> datepat.findall(text)
[('11', '27', '2012'), ('3', '13', '2013')]
>>> for month, day, year in datepat.findall(text):
... print('{}-{}-{}'.format(year, month, day))
...
2012-11-27
2013-3-13
```

##### group , groups
```
>>> detepat = re.compile(r'(\d+)/(\d+)/(\d+)')
>>> m = detepat.match('11/27/2014')
>>> m
<_sre.SRE_Match object; span=(0, 10), match='11/27/2014'>
>>> m.group(0)
'11/27/2014'
>>> m.group(1)
'11'
>>> m.group(2)
'27'
>>> m.group(3)
'2014'
>>> m.groups()
('11', '27', '2014')
>>> month , day , year = m.groups()
>>> day
'27'
>>> month
'11'
>>> year
'2014'
```


##### startswith, endswitch , listdir
```
>>> import os
>>> filenames = os.listdir('.')
>>> filenames
[ 'Makefile', 'foo.c', 'bar.py', 'spam.c', 'spam.h' ]
>>> [name for name in filenames if name.endswith(('.c', '.h')) ]
['foo.c', 'spam.c', 'spam.h'
>>> any(name.endswith('.py') for name in filenames)
True
```


##### re.sub
```
>>> text = 'Today is 11/27/2012. PyCon starts 3/13/2013.'
>>> import re
>>> re.sub(r'(\d+)/(\d+)/(\d+)', r'\3-\1-\2', text)
'Today is 2012-11-27. PyCon starts 2013-3-13.'
```


-- 忽略大小写
```
>>> text = 'UPPER PYTHON, lower python, Mixed Python'
>>> re.findall('python', text, flags=re.IGNORECASE)
['PYTHON', 'python', 'Python']
>>> re.sub('python', 'snake', text, flags=re.IGNORECASE)
'UPPER snake, lower snake, Mixed snake'
```

##### fnmatch , fnmatchcase 
```
>>> from fnmatch import fnmatch , fnmatchcase
>>> fnmatch('foo.txt' , '*.txt')
True
>>> fnmatch('foo.txt' , '?oo.txt')
True
>>> fnmatch('date667','date[0-9]*')
True
>>> names = ['dat1.csv', 'dat2.nin' , 'foo.py']
>>> [name for name in names if fnmatch(name , 'dat*.csv')]
['dat1.csv']
>>> fnmatch('foo.txt' , '*.TXT')
True
>>> fnmatch('foo.txt' , '*.TXT')
True
>>> fnmatchcase('foo.txt' , '*.TXT')
False
>>> fnmatchcase('foo.txt' , '*.txt')
True
```

#### calendar 日历模块的使用
```
>>> from calendar import month_abbr
>>> def change_date(m):
... mon_name = month_abbr[int(m.group(1))]
... return '{} {} {}'.format(m.group(2), mon_name, m.group(3))
...
>>> datepat.sub(change_date, text)
'Today is 27 Nov 2012. PyCon starts 13 Mar 2013.'
```

#### unicodedata 处理unicode 字符串
```
>>> import unicodedata
>>> t1 = unicodedata.normalize('NFC', s1)
>>> t2 = unicodedata.normalize('NFC', s2)
>>> t1 == t2
True
>>> print(ascii(t1))
'Spicy Jalape\xf1o'
>>> t3 = unicodedata.normalize('NFD', s1)
>>> t4 = unicodedata.normalize('NFD', s2)
>>> t3 == t4
True
>>> print(ascii(t3))
'Spicy Jalapen\u0303o'

>>> s = '\ufb01' # A single character
>>> s
' fi '
>>> unicodedata.normalize('NFD', s)
' fi '
#Notice how the combined letters are broken apart here
>>> unicodedata.normalize('NFKD', s)
'fi'
>>> unicodedata.normalize('NFKC', s)
'fi'

注：normalize() 第一个参数指定字符串标准化的方式。NFC 表示字符应该是整体组
成 (比如可能的话就使用单一编码)，而 NFD 表示字符应该分解为多个组合字符表示。
Python 同样支持扩展的标准化形式 NFKC 和 NFKD，它们在处理某些字符的时候
增加了额外的兼容特性
```

#### strip 删除多余字符
```
>>> s = ' hello world \n'
>>> s.strip()
'hello world'
>>> s.lstrip()
'hello world \n'
>>> s.rstrip()
' hello world'
>>>
>>> # Character stripping
>>> t = '-----hello====='
>>> t.lstrip('-')
'hello====='
>>> t.strip('-=')
'hello'
```


