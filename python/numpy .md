```

import numpy as np

```

#### 绘图

```
x = np.linspace(0, 3, 20)
y = np.linspace(0, 9, 20)

# 线图
plt.plot(x, y)       

＃ 点图
plt.plot(x, y, 'o')	

```

#### 绘制2D 图

```

>>> image = np.random.rand(30, 30)
>>> plt.imshow(image, cmap=plt.cm.hot)
<matplotlib.image.AxesImage object at 0x11097d7d0>
>>> plt.colorbar()
<matplotlib.colorbar.Colorbar object at 0x110a12410>
>>> plt.show()
>>> 

```



#### numpy array

```
np.array([0, 1, 3, 2])

```

#### numpy arange 

```

np.arange(10000)

#数组切片 
>>> a = np.arange(10)

＃[开始:结束:步长]
>>> a[2:9:3]

array([2, 5, 8])

```

#### numpy arr-func

```
#查看 array系列函数
np.lookfor('create array')

```

#### numpy linspace 

```
In [76]: c = np.linspace(0, 1, 6)

In [77]: c
Out[77]: array([ 0. ,  0.2,  0.4,  0.6,  0.8,  1. ])

```

#### numpy ones

```
In [82]: np.ones((3, 3))		#(3, 3) 元组
Out[82]: 
array([[ 1.,  1.,  1.],
       [ 1.,  1.,  1.],
       [ 1.,  1.,  1.]])

```

#### numpy zeros

```
#创建元素值为0 的元组数组
In [83]: np.zeros((2, 2))
Out[83]: 
array([[ 0.,  0.],
       [ 0.,  0.]])


```

#### numpy eye

```
#对角元组
In [84]: np.eye(3)
Out[84]: 
array([[ 1.,  0.,  0.],
       [ 0.,  1.,  0.],
       [ 0.,  0.,  1.]])

```


#### numpy diag

```
#对角递增
In [85]: np.diag(np.array([1, 2, 3, 4]))
Out[85]: 
array([[1, 0, 0, 0],
       [0, 2, 0, 0],
       [0, 0, 3, 0],
       [0, 0, 0, 4]])


```


#### numpy random

```

＃高斯
In [87]: np.random.randn(4)
Out[87]: array([ 1.09941861,  1.09663985,  0.7709997 ,  0.03094098])

#均匀分布
In [88]: np.random.rand(4)
Out[88]: array([ 0.4393972 ,  0.81030029,  0.86413102,  0.9170734 ])

#设置随机种子
np.random.seed(1234)

```

#### numpy dtype 数据类型

```

#数据类型 ＝＝> 整数
In [93]: a = np.array([1, 2, 3])

In [94]: a.dtype
Out[94]: dtype('int64')


#数据类型 ＝＝> 浮点数
In [95]: b = np.array([1., 2., 3.])

In [96]: b.dtype
Out[96]: dtype('float64')


#数据类型 ＝＝> 复数
In [100]: d = np.array([1+2j, 2+3j, 5+6*1j])

In [101]: d.dtype
Out[101]: dtype('complex128')

#数据类型 ＝＝> bool
In [102]: np.array([True, False]).dtype
Out[102]: dtype('bool')

#数据类型 ＝＝> 字符串
In [105]: np.array(['Hello', 'World', 'Numpy.array']).dtype
Out[105]: dtype('S11')		=> 'Numpy.array' => 11 个字符


#设置 dtype
	In [97]: c = np.array([1, 2, 3], dtype=float)

	In [98]: c
	Out[98]: array([ 1.,  2.,  3.])
	
	In [99]: c.dtype
	Out[99]: dtype('float64')

```