

#### 函数的传参
- 让一个函数接受任意数量的位置参数，可以使用一个 * 参数
def avg(first , *rest):
	return (first + sum(rest)) / (1 + len(rest))
print(avg(1,2,3))

- 为了接受任意数量的关键字参数，使用一个以 ** 开头的参数
```
import html
def make_element(name , value , **attrs):
		keyvals = [' %s="%s"' % item for item in attrs.items()]
		attr_str = ''.join(keyvals)
		element = '<{name}{attrs}>{value}</{name}>'.format(name=name , attrs=attr_str  , value=html.escape(value))
		return element

str = make_element('item' , 'Albatross' , size="large" , quantity=6)
p   = make_element('p' , '<spam>')

只接受关键字参数的函数
def mininum(*values , clip=None):
	m = min(values)
	if clip is not None:
		m = clip if clip > m else m 
	return m

minnum = mininum(1,23,43,4,34,3,4, clip=3)
print(minnum)
```

- 函数参数注解
```
>>> def add(x:int , y:int)->int:
...     return x+y
...
>>> str = add(2,3)
>>> str
5
>>> help(add)
Help on function add in module __main__:

add(x:int, y:int) -> int

>>> add.__annotations__
{'y': <class 'int'>, 'return': <class 'int'>, 'x': <class 'int'>}
```

#### 匿名或内联函数
```
lambda
>>> add = lambda x, y: x + y
>>> add(2,3)
5
```

- lambad 遇到自由变量时
```
>>> x =10
>>> a = lambda y : x +y
>>> x = 20
>>> b = lambda y:x+ y
>>> a(10)
30
>>> b(10)
30
>>>
```

- 如果你想让某个匿名函数在定义时就捕获到值，可以将那个参数值定义成默认参数
即可，就像下面这样：
```
>>> x = 10
>>> a = lambda y, x=x: x + y
>>> x = 20
>>> b = lambda y, x=x: x + y
>>> a(10)
20
>>> b(10)
30
```

- partial() 
函数允许你给一个或多个参数设置固定的值，减少接下来被调用时的参数个数
```
def spam(a, b, c, d):
print(a, b, c, d)

>>> from functools import partial
>>> s1 = partial(spam, 1) # a = 1
>>> s1(2, 3, 4)
1 2 3 4
>>> s1(4, 5, 6)
1 4 5 6
>>> s2 = partial(spam, d=42) # d = 42
>>> s2(1, 2, 3)
1 2 3 42
>>> s2(4, 5, 5)
4 5 5 42
>>> s3 = partial(spam, 1, 2, d=42) # a = 1, b = 2, d = 42
>>> s3(3)
1 2 3 42
>>> s3(4)
1 2 4 42
```

- 回调函数的使用
```
def  apply_async(func, args, *, callback):
result = func(*args)
callback(result)

>>> def print_result(result):
... print('Got:', result)
 
>>> def add(x, y):
... return x + y

>>> apply_async(add, (2, 3), callback=print_result)
Got: 5
>>> apply_async(add, ('hello', 'world'), callback=print_result)
Got: helloworld
```

### 闭包函数
```
#闭包函数
def sample():
	n = 0
	def func():
		print('n=' , n)

	def get_n():
		return n

	def set_n(value):
		nonlocal n
		n =value

	func.get_n = get_n
	func.set_n = set_n
	return func

f = sample()
f.set_n(1999)
print(f.get_n())
```

nonlocal 声明可以让我们编写函数来修改内部变量的值

```
-- dmo --
import sys
class ClosureInstance:
	def __init__(self , locals=None):
		if locals is None:
			locals = sys._getframe(1).f_locals

		self.__dict__.update((key ,value) for key , value in locals.items() if callable(value))

	def __len__(self):
		return self.__dict__['__len__']()

def Stack():
	items = [] 
	def push(item):
		items.append(item)

	def pop():
		return items.pop()

	def __len__():
	 	return len(items)

	return ClosureInstance()


s = Stack()
s.push(10)
print(s.pop())
```


### Python 面向对象

- __solts__ 

```
class Date:
	__slots__ = ['year','month','day']

	def __init__(self , year , month ,day):
		self.year 	= year
		self.month 	= month
		self.day 	= day
```
    当你定义 slots 后，Python 就会为实例使用一种更加紧凑的内部表示。实例通
    过一个很小的固定大小的数组来构建，而不是为每个实例定义一个字典，这跟元组或列表很类似。
    
    在 slots 中列出的属性名在内部被映射到这个数组的指定小标上。使用 slots 一个不好的地方就是我们不能再给实例添加新的属性了，只能使用在 slots 中定义的那些属性名。
    
    关于 slots 的一个常见误区是它可以作为一个封装工具来防止用户给实例增新的属性。尽管使用 slots 可以达到这样的目的，但是这个并不是它的初衷。 slots
    更多的是用来作为一个内存优化工具。

### @property 装饰器

```
from decimal import Decimal 

class Fees(object):
	def __init__(self):
		self._fee = None

	@property
	def fee(self):
	    return self._fee

	@fee.setter
	def fee(self, value):
		self._fee = value

if __name__ == '__main__':
	f = Fees()
	f.fee = 'zeopean'
	print(f.fee)

super
class Base:
	def __init__(self):
		print('Base.__init__')

class A(Base):
	def __init__(self):
		super().__init__()
		print('A.__init__')

class B(Base):
	def __init__(self):
		super().__init__()
		print('B.__init__')

class C(A ,B):
	def __init__(self):
		super().__init__()
		print('C.__init__')

if __name__ == '__main__':
	c = C()
	print(c)

super property
class String:
	def __init__(self ,name):
		self.name = name 

	def __get__(self, instance , cls):
		if instance is None:
			return self
		return instance.__dict__[self.name]


	def __set__(self , instance , value):
		if not instance(value , str):
			raise TypeError("Expected a string")
		instance.__dict__[self.name] = value


class Person:
	name = String('name')

	def __init__(self , name):
		self.name = name


class SubPerson(Person):
	@property
	def name(self):
	    print("getting name")
	    return super().name

	@name.setter
	def name(self, value):
	    print("setting name to " , value)
	    super(SubPerson , SubPerson).name.__set__(self ,value)

    @name.deleter
    def name(self):
    	print("deleteing name")
    	super(SubPerson ,SubPerson).name.__delete__(self)

	
if __name__ == "__main__":
	print(SubPerson())

```


### @lazyproperty
```
class lazyproperty:
	def __init__(self, func):
		self.func = func
	
	def __get__(self, instance, cls):
		if instance is None:
			return self
		else:
			value = self.func(instance)
			setattr(instance, self.func.__name__, value)
			return value


import math

class Circle:
	def __init__(self , radius):
		self.radius = radius

	@lazyproperty
	def area(self):
		print("computing area")
		return math.pi * self.radius ** 2


	@lazyproperty
	def perimeter(self):
		print("computing perimeter")
		return 2 * math.pi * self.radius

if __name__ == '__main__':
	c= Circle(34)
	print(c.radius)
	print(c.area)
	print(c.perimeter)
```

- 定义公用的 __init__ 简化数据架构

```
import math
class Structure:
    _fields = []
    def __init__(self , *args):
        if len(args) != len(self._fields):
            raise TypeError("Expected {} arguments ".format(len(self._fields)))
        for name , value in zip(self._fields , args):
            setattr(self , name ,value)
class Stock(Structure):
    _fields = ['name' , 'age' , 'address']
class Point(Structure):
    _fields = ['x' ,'y']
class Circle(Structure):
    _fields = ['radius']
    def area(self):
        return math.pi * self.radius ** 2
if __name__ == "__main__":
    s = Stock('zeopeab' ,23 , '1212@11.cpm')
    p = Point(2 ,3);
    c = Circle(45)
    print(s)
    print(p)
    print(c)
```
