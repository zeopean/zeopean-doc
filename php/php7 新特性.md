#### ?? 的使用

```
$username = $name ?? "daming";  //daming

等同

$username = isset($name) ? $name : "daming";

```

#### random_?? 的使用

```
random_bytes(int length);
random_int(int min, int max);

``` 


#### <=> 的使用

```

php> echo 1 <=> 1.2;
-1
php> echo 1 <=> -1.2;
1


```

#### intdiv 的使用

```
php> var_dump(intdiv("1232.e10", 1));
int(12320000000000)

```

#### 参数类型说明

	默认情况下，所有的PHP文件都处于弱类型校验模式。新的declare指令，通过指定strict_types的值（1或者0），1表示严格类型校验模式，作用于函数调用和返回语句；0表示弱类型校验模式。


```
declare(strict_types=1);

```


#### 类常量属性设定

这个特性说起来比较简单，就是现在类中的常量支持使用 public、private 和 protected 修饰了：

```
	<?php
	class Token {
	    // 常量默认为 public
	    const PUBLIC_CONST = 0;
	
	    // 可以自定义常量的可见范围
	    private const PRIVATE_CONST = 0;
	    protected const PROTECTED_CONST = 0;
	    public const PUBLIC_CONST_TWO = 0;
	
	    // 多个常量同时声明只能有一个属性
	    private const FOO = 1, BAR = 2;
	}
```

此外，接口（interface）中的常量只能是 public 属性：

```
	<?php
	interface ICache {
	    public const PUBLIC = 0;
	    const IMPLICIT_PUBLIC = 1;
	}
```	

#### void 返回类型

PHP7.0 添加了指定函数返回类型的特性，但是返回类型却不能指定为 void，7.1 的这个特性算是一个补充：

```
	<?php
	function should_return_nothing(): void {
	    return 1; // Fatal error: A void function must not return a value
	}
```
以下两种情况都可以通过验证：

```
	<?php
	function lacks_return(): void {
	    // valid
	}
	
	function returns_nothing(): void {
	    return; // valid
	}
```
	
定义返回类型为 void 的函数不能有返回值，即使返回 null 也不行：

```
	<?php
	function returns_one(): void {
	    return 1; // Fatal error: A void function must not return a value
	}
	
	function returns_null(): void {
	    return null; // Fatal error: A void function must not return a value
	}

```

此外 void 也只适用于返回类型，并不能用于参数类型声明，或者会触发错误：

```
	<?php
	function foobar(void $foo) { // Fatal error: void cannot be used as a parameter type
	}
```

类函数中对于返回类型的声明也不能被子类覆盖，否则会触发错误：

```
	<?php
	class Foo
	{
	    public function bar(): void {
	    }
	}
	
	class Foobar extends Foo
	{
	    public function bar(): array { // Fatal error: Declaration of Foobar::bar() must be compatible with Foo::bar(): void
	    }
	}
```	





#### PHP7 弃用功能
核心：
• PHP4风格的构造函数将被弃用。(和类名同名的方法视为构造方法，这是 PHP4的语法。)
• 静态调用非静态方法将被弃用。

####  PHP7 修改的函数

	parse_ini_file()和 parse_ini_string()的 scanner_mode 参数增加了 INI_SCANNER_TYPED 选项。
	
	unserialize()增加了第二个参数，可以用来指定接受的类列表。RFC: https://wiki.php.net/rfc/secure_unserialize
	 
	proc_open()打开的最大限制之前是写死的16，现在这个限制被移除了，最大数量取决于 PHP 可用的内存。windows版本增加了选项"blocking_pipes"，可用来指定是否强制以块的方式读取。
	 
	array_column():The function now supports an array of objects as well as two-dimensional arrays
	 
	stream_context_create()windows 下面可以接收 array("pipe" => array("blocking" => <boolean>))参数。
	 
	dirname()增加了可选项$levels，可以用来指定目录的层级。dirname(dirname($foo)) => dirname($foo, 2);
	 
	debug_zval_dump()打印的时候，使用 int 代替 long，使用 float 代替 double。


#### PHP7 新增函数

	GMP 模块新增了 gmp_random_seed()函数。
	
	PCRE 增加了 preg_replace_callback_array 方法。RFC: https://wiki.php.net/rfc/preg_replace_callback_array
	
	增加了 intdiv()函数。
	
	增加了 error_clear_last()函数来重置错误状态。
	
	增加了 ZipArchive::setComapressionIndex()和 ZipArchive::setCompressionName()来设置压缩方法。

	增加了 deflate_init(), deflate_add(), inflate_init(), inflate_add()。


#### PHP7 其他修改
	
	NaN 和 Infinity 转为整型的时候，始终为0。
		
	Calling a method on a non-object 现在会抛出一个可以扑获的错误，不再是致命错误。
	https://wiki.php.net/rfc/catchable-call-to-member-of-non-object
		
	zend_parse_parameters 的错误信息始终使用 integer, float，不再使用 long 和 double。
		
	ignore_user_abort 设为真的话，输出缓存会继续工作，即使链接中断。
		
	Zend 扩展接口使用 zend_extension.op_array_persist_calc()和 zend_extensions.op_array_persist() 。
		
	引入了 zend_internal_function.reserved[]数组