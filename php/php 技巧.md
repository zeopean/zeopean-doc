#### extension_loaded 

    检查一个扩展是否已经加载

#### strncmp

    二进制安全比较字符串开头的若干个字符


#### array_column 

    返回数组中指定的一列


#### array_rand($arr, $len) 从数组中随机取出一个或多个单元
```
注意：当$arr的长度，小于$len 时，会出现错误

```




#### array_fill_keys() 使用指定的键和值填充数组
```
<?php
$keys = array('foo', 5, 10, 'bar');
$a = array_fill_keys($keys, 'banana');
print_r($a);


#以上例程会输出：

Array
(
    [foo] => banana
    [5] => banana
    [10] => banana
    [bar] => banana
)
```


#### 1. call_user_func  && call_user_func_array
    
    * 调用由第一参数给出的回调函数，并将其余的参数作为回调函数的参数。
    * call_user_func_array 表示参数为数组
```
class TestFunCallUserFunc
{
    public function index($arg1)
    {
        echo $arg1;
        echo '<br>';
    }
}


call_user_func(['TestFunCallUserFunc', 'index'],'zeopean');
#retult: zeopean

function _testCallUserFunc($arg)
{
    echo $arg;
}

call_user_func('_testCallUserFunc', 'daming');


echo '<hr>';

call_user_func_array(['TestFunCallUserFunc', 'index'], ['zeopean']);
echo '<hr>';

call_user_func_array('_testCallUserFunc', ['daming']);

#result: daming
```
    
#### 2. call_user_func_array 
    
    * 调用由第一参数给出的回调函数，并将数组param_arr的参数作为回调函数的参数。

    1. NOTE: 
        1. 需要注意的一点事，call_user_func（）的回调函数参数不能通过引用传递，而 call_user_func_array ()是可以的。比如下面这个例子：
        
        2. 在函数中注册有多个回调内容时(如使用 call_user_func() 与 call_user_func_array())，如在前一个回调中有未捕获的异常，其后的将不再被调用。
         
    
    2. 参考文章：
    
    * http://blog.csdn.net/risingsun001/article/details/21696585


#### 3.创建一个空对象的三种方式
```php
<?php
    $obj1 = new \stdClass; // Instantiate stdClass object
    $obj2 = new class{}; // Instantiate anonymous class
    $obj3 = (object)[]; // Cast empty array to object
    
    var_dump($obj1); // object(stdClass)#1 (0) {}
    var_dump($obj2); // object(class@anonymous)#2 (0) {}
    var_dump($obj3); // object(stdClass)#3 (0) {}
?>

```

#### 4.array_flip 数组键值对换
```
array array_flip ( array $trans )
array_flip() 返回一个反转后的 array，例如 trans 中的键名变成了值，而 trans 中的值成了键名。

注意 trans 中的值需要能够作为合法的键名，例如需要是 integer 或者 string。如果值的类型不对将发出一个警告，并且有问题的键／值对将不会反转。

如果同一个值出现了多次，则最后一个键名将作为它的值，所有其它的都丢失了。
```
```php
<?php
    $trans = array("a" => 1, "b" => 1, "c" => 2);
    $trans = array_flip($trans);
    print_r($trans);
?>

```


#### 5.array_intersect_key 使用键名比较计算数组的交集
```
array array_intersect_key ( array $array1 , array $array2 [, array $ ... ] )
array_intersect_key() 返回一个数组，该数组包含了所有出现在 array1 中并同时出现在所有其它参数数组中的键名的值。

```

#### 6.get_class_methods 返回由类的方法名组成的数组

```
array get_class_methods ( mixed $class_name )
返回由类的方法名组成的数组
```

#### 7.get_called_class   后期静态绑定（"Late Static Binding"）类的名称

```php
<?php

class foo {
    static public function test() {
        var_dump(get_called_class());
    }
}

class bar extends foo {
}

foo::test();
bar::test();

?>

->'foo'
->'bar'
```


#### 8.func_get_args  函数的任意数目的参数



#### 9.glob() 查找文件 


#### 10.gzcompress() 和 gzuncompress() 函数 字符串压缩


#### 11.gethostbyname  gethostbynamel  gethostbyadd  获取ip地址

```php
    $ip = gethostbyname('www.baidu.com');		//获取单个ip地址
    echo $ip;			//文本形式
    
    $ip1 = gethostbynamel('www.pgzhe.com');		//获取多个ip地址
    var_dump($ip1);		//数组形式
    
    $hostname = gethostbyaddr('192.168.199.233');  //获取主机名
    
    echo $hostname;
```


#### 12.feof 检测是否已到达文件末尾 (eof)
```
    如果文件指针到了 EOF 或者出错时则返回 TRUE，否则返回一个错误（包括 socket 超时），其它情况则返回 FALSE。
    # 语法
    feof(file)
    
    # 参数	描述
    file	必需。规定要检查的打开文件。
    
    # 说明
    file 参数是一个文件指针。这个文件指针必须有效，并且必须指向一个由 fopen() 或 fsockopen() 成功打开（但还没有被 fclose() 关闭）的文件。
    
    # 提示和注释
    提示：feof() 函数对遍历长度未知的数据很有用。
    注意：如果服务器没有关闭由 fsockopen() 所打开的连接，feof() 会一直等待直到超时而返回 TRUE。默认的超时限制是 60 秒，可以使用 stream_set_timeout() 来改变这个值。
    注意：如果传递的文件指针无效可能会陷入无限循环中，因为 EOF 不会返回 TRUE。
```
```php
<?php
    $file = fopen('http://www.baidu.com/', "r");
    //输出文本中所有的行，直到文件结束为止。
    while(! feof($file))
      {
      echo fgets($file). "<br />";
      }
    
    fclose($file);
```


#### 13.uniqid() 函数
- 定义和用法
        
        uniqid() 函数基于以微秒计的当前时间，生成一个唯一的 ID。
        
    语法
        uniqid(prefix,more_entropy)
        
        参数	描述
        prefix	可选。为 ID 规定前缀。如果两个脚本恰好在相同的微秒生成 ID，该参数很有用。
        more_entropy	可选。规定位于返回值末尾的更多的熵。
        
        说明
        如果 prefix 参数为空，则返回的字符串有 13 个字符串长。如果 more_entropy 参数设置为 true，则是 23 个字符串长。
        
        如果 more_entropy 参数设置为 true，则在返回值的末尾添加额外的熵（使用组合线形同余数生成程序），这样可以结果的唯一性更好。
        返回值
        以字符串的形式返回唯一标识符。
        提示和注释
        注释：由于基于系统时间，通过该函数生成的 ID 不是最佳的。如需生成绝对唯一的 ID，请使用 md5() 函数（请在字符串函数参考中查找）。

#### 14.list() 函数

- 定义和用法
```
    list() 函数用数组中的元素为一组变量赋值。
    注意，与 array() 类似，list() 实际上是一种语言结构，不是函数。
    
    语法
    list(var1,var2...)
    
    参数	描述
    var1	必需。第一个需要赋值的变量。
    var2	可选。可以有多个变量。
    
    提示和注释
    注释：该函数只用于数字索引的数组，且假定数字索引从 0 开始。
```
```
<?php
    $my_array = array("Dog","Cat","Horse");
    
    list($a, $b, $c) = $my_array;
    echo "I have several animals, a $a, a $b and a $c.";

#输出：
    I have several animals, a Dog, a Cat and a Horse.
```

#### 15.array_map() 函数

- 定义和用法
```
    array_map() 函数返回用户自定义函数作用后的数组。回调函数接受的参数数目应该和传递给 array_map() 函数的数组数目一致。
    
    语法
    array_map(function,array1,array2,array3...)
    
    参数	描述
    function	必需。用户自定义函数的名称，或者是 null。
    array1	必需。规定数组。
    array2	可选。规定数组。
    array3	可选。规定数组。
```
```php
<?php
    function myfunction($v) 
    {
    if ($v==="Dog")
    {
    	return "Fido";
    }
    return $v;
    }
    $a=array("Horse","Dog","Cat");
    print_r(array_map("myfunction",$a));
    
输出：
    Array ( [0] => Horse [1] => Fido [2] => Cat )

```

#### 16.array_filter() 函数
- 定义和用法
```
    array_filter() 函数用回调函数过滤数组中的元素，如果自定义过滤函数返回 true，则被操作的数组的当前值就会被包含在返回的结果数组中， 并将结果组成一个新的数组。如果原数组是一个关联数组，键名保持不变。
    
    语法
    array_filter(array,function)
    
    参数	描述
    array	必需。规定输入的数组。
    function	必需。自定义函数的名称。
```
```php
<?php
    function myfunction($v) 
    {
    if ($v==="Horse")
    	{
    	return true;
    	}
    return false;
    }
    $a=array(0=>"Dog",1=>"Cat",2=>"Horse");
    print_r(array_filter($a,"myfunction"));
?>
输出：
    Array ( [2] => Horse )
```


#### 17.fsockopen 

#### 18.array_multisort 对二维数组进行排序

```
bool array_multisort ( array &$arr [, mixed $arg = SORT_ASC [, mixed $arg = SORT_REGULAR [, mixed $... ]]] )

array_multisort() 可以用来一次对多个数组进行排序，或者根据某一维或多维对多维数组进行排序。

关联（string）键名保持不变，但数字键名会被重新索引。
```

```

    /**
     * ======================================================================
     * @param $lists
     * @return array
     * 二维数组降序排序
     */
    private function sortStatisticList($lists)
    {
        if(empty($lists))
            return [];

        $tmp = [];
        //提取列数组
        foreach ($lists as $key => $val) {
            $tmp[$key] = (float)$val['total'];
        }
        array_multisort($tmp,SORT_DESC,$lists);    //此处对数组进行降序排列；SORT_DESC按降序排列
        return $lists;
    }
    
```
