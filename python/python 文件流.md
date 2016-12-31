
#### open | write | read
```py
>>> with open('demo.txt' , 'wt') as f:  		#以文本(wt)形式写入操作
...     f.write("hello guohai")
12
>>> with open('demo.txt' , 'rt') as f:		#以文本(rt)形式读取操作
...     data = f.read()
>>> data
'hello guohai'
>>> with open('demo.txt' , 'at') as f:		#以文本(at)形式追加操作
...     f.write('hello zeopean')
13
>>> with open('demo.txt' , 'rt') as f:
...     data = f.read()
>>> data
'hello guohaihello zeopean'
```


#### print 输出到文件中
```py
with open('d:/work/test.txt', 'wt') as f:
print('Hello World!', file=f)
```

#### 二进制读写

如果你想从二进制模式的文件中读取或写入文本数据，必须确保要进行解码和编码
操作。比如：

```py
with open('somefile.bin', 'rb') as f:
data = f.read(16)
text = data.decode('utf-8')
with open('somefile.bin', 'wb') as f:
text = 'Hello World'
f.write(text.encode('utf-8'))
```


#### 判断文件是否存在
```py
>>> import os
>>> if not os.path.exists('somefile'):
... with open('somefile', 'wt') as f:
... f.write('Hello\n')
... else:
... print('File already exists!')
...
File already exists!
```


#### StringIO | BytesIO
##### StringIO
```py
>>> s = io.StringIO()
>>> s.write('Hello World\n')
12
>>> print('This is a test', file=s)
15
>>> s.getvalue()
'Hello World\nThis is a test\n'
>>>
>>> s = io.StringIO('Hello\nWorld\n')
>>> s.read(4)
'Hell'
>>> s.read()
'o\nWorld\n'
>>>
```


##### BytesIO
```py
>>> s = io.BytesIO()
>>> s.write(b'binary data')
>>> s.getvalue()
b'binary data'
>>>
```


#### readinto | bytearray | memoryview
```py
record_size = 32  
buf = bytearray(record_size)
with open('somefile', 'rb') as f:
while True:
n = f.readinto(buf)
if n < record_size:
break

# 另外有一个有趣特性就是 memoryview ，它可以通过零复制的方式对已存在的缓冲区执行切片操作，甚至还能修改它的内容。比如：

```

```py
>>> buf
bytearray(b'Hello World')
>>> m1 = memoryview(buf)
>>> m2 = m1[-5:]
>>> m2
<memory at 0x100681390>
>>> m2[:] = b'WORLD'
>>> buf
bytearray(b'Hello WORLD')
```
 
#### mmap 内存映射的二进制文件
```py
import os
import mmap

def memory_map(filename , access=mmap.ACCESS_WRITE):
	size = os.path.getsize(filename)
	fd = os.open(filename , os.O_RDWR)
	return mmap.mmap(fd ,size , access=access)

size = 1000000
with open('data' , 'wb') as f:
	f.seek(size - 1)
	f.write(b'\x00')

m = memory_map('data')
print(len(m))

print(m[0:10])

# print(b'hello daming' , file=m[0:11])
# m.close()

with open('data' ,'rb') as f:
	print(f.read(11))
```
#### os.path

##### basename | dirname | join | splitext | expanduser

```py
import os
>>> path = 'demo.bin'
>>> os.path.basename(path)		#文件名
'demo.bin'
>>> os.path.dirname(path)		#文件路径
''
>>> os.path.join('tmp','data' , os.path.basename(path))  #路径拼接
'tmp\\data\\demo.bin'
>>> path = '~/data/data.bin'
>>> os.path.expanduser(path)	#系统路径
'C:\\Users\\Administrator/data/data.bin'
>>> os.path.splitext(path)		#获取后缀名
('~/data/data', '.bin')
```


##### exists | isdir | islink | realpath
```py
os.path.exists('/etc/passwd')  	#判断文件是否存在
>>> os.path.isdir('user.data') 	#判断是否是目录
False
>>> os.path.islink('demo.bin') 	#判断是否是超链接
False
>>> os.path.realpath('demo.bin') #获取文件的绝对路径
'E:\\zeopean\\pycode\\pyfunc\\demo.bin'
```


##### getmtime | getsize 获取元数据
```py
>>> os.path.getmtime('demo.txt')
1459387735.7783203
>>> import time
>>> time.ctime(os.path.getmtime('demo.bin'))
'Thu Mar 31 10:27:36 2016'
>>> os.path.getsize('demo.txt')
47
```

#####  listdir 
```py
>>> names = os.listdir('.')
>>> names
['closure.func.py', 'closureInstance.py', 'data', 'demo.bin', 'demo.txt', 'file.
txt', 'make_element.py', 'mmap.demo.py', 'readinto.demo.py', 'yield.func.py']
```


##### tempfile
--临时文件 TemporaryFile
```py
from tempfile import TemporaryFile
f = TemporaryFile('w+t')
# Use the temporary file
...
f.close()
```


##### 有名字的临时文件 NamedTemporaryFile
```py
from tempfile import NamedTemporaryFile
with NamedTemporaryFile('w+t') as f:
print('filename is:', f.name)
```


##### 临时目录 TemporaryDirectory
```py
from tempfile import TemporaryDirectory
with TemporaryDirectory() as dirname:
print('dirname is:', dirname) 
```


#####  插件临时文件 mkstemp | mkdtemp
```py
>>> import tempfile
>>> tempfile.mkstemp()
(3, 'C:\\Users\\ADMINI~1\\AppData\\Local\\Temp\\tmp_jbpp74i')
>>> tempfile.mkdtemp()
'C:\\Users\\ADMINI~1\\AppData\\Local\\Temp\\tmpkwsqedpa'
```


##### 获取临时文件名  gettempdir
```py
import tempfile
tempfile.gettempdir()
'C:\\Users\\ADMINI~1\\AppData\\Local\\Temp'
```

#### Pickle

- 序列化对象
```py

>>> import pickle
>>> f = open('somedata', 'wb')
>>> pickle.dump([1, 2, 3, 4], f)
>>> pickle.dump('hello', f)
>>> pickle.dump({'Apple', 'Pear', 'Banana'}, f)
>>> f.close()
>>> f = open('somedata', 'rb')
>>> pickle.load(f)
[1, 2, 3, 4]
>>> pickle.load(f)
'hello'
>>> pickle.load(f)
{'Apple', 'Pear', 'Banana'}

```
