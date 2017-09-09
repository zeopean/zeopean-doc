
irb 进入irb模式

### 安装gem 
```
sudo gem install -n /usr/local/bin ruby-debug-ide  

```
### rvm 镜像选择

```
echo "ruby_url=https://cache.ruby-china.org/pub/ruby" > ~/.rvm/user/db

```


ruby 数据类型
---

### 字符串



字符串

```
string = "Hello, Hello zeopean!"
=> "Hello, Hello zeopean!"

string.gsub("Hello", "hi")
=> "hi, hi zeopean!"

string.sub("Hello", "hi")
=> "hi, Hello zeopean!"

```

获取字符串长度

```
string = "hello"
string.length // 获取长度
```

字符串分解

```
string.split

```


字符串模板使用

```

字符串插值仅适用于双引号字符串。在字符串内使用插值标记#{}。

modifier = "ok "
puts "I am #{modifier * 3 }"

```

获取随机字符串

```
>> ('a'..'z').to_a                     # 由全部英文字母组成的数组
=> ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o",
"p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"]
>> ('a'..'z').to_a.shuffle             # 打乱数组
=> ["c", "g", "l", "k", "h", "z", "s", "i", "n", "d", "y", "u", "t", "j", "q",
"b", "r", "o", "f", "e", "w", "v", "m", "a", "x", "p"]
>> ('a'..'z').to_a.shuffle[0..7]       # 取出前 8 个元素
=> ["f", "w", "i", "a", "h", "p", "c", "x"]
>> ('a'..'z').to_a.shuffle[0..7].join  # 把取出的元素合并成字符串
=> "mznpybuj"

```


循环的使用

```

    5.times do
      puts "hello world"
    end
    
    4.times{puts "daming"}

    5.times do |i|
      puts "hello dami#{i}"
    end
```


### 数组

```

  arrays = ["daming", 1, false]
  puts arrays
  
  # 数组截取
  meals[2]
  
  # 截取最后一个元素
  meals.last
  
  # 排序
  meals.sort
  
  # push 方法向数组中添加元素
  arrays.push("da")
  a << "foo" << "bar"        # 串联操作
  
  # 数组转转发串
  arrays.join(", ")
  
```

### Hash 散列

* 创建一个散列，三种方式同效

```
> hash1 = Hash.new
 => {} 
 
> hash2 = Hash.new(0)
 => {} 
 
> hash1 == hash2
 => true 
 
> hash3 = {}
 => {} 
 
> hash1 == hash3
 => true 

```




### 值域


```

(0..9).to_a            # 调用 to_a 时要用括号包住值域

>> a = %w[foo bar baz quux]         # %w 创建一个元素为字符串的数组
=> ["foo", "bar", "baz", "quux"]
>> a[0..2]
=> ["foo", "bar", "baz"]

```


### 键值对

```

pro = {"apple" => 3, "orange" => 2, "carrots" => 3}
=> {"apple"=>3, "orange"=>2, "carrots"=>3}

irb(main):019:0> pro["apple"]
=> 3

irb(main):020:0> pro["apple"]="dam"
=> "dam"

irb(main):021:0> pro
=> {"apple"=>"dam", "orange"=>2, "carrots"=>3}

```


ruby 变量
---

特性 |	局部变量 |	全局变量 |	实例变量 |	类变量
--- | --- | --- | --- | --- 
范围 |	仅限于初始化块内 |	全局范围 |	属于一个类的一个实例 | 仅限于创建它们的整个类
命名约定	|以小写字母或下划线(_)开头	|以$符号开头 | 以@符号开头 | 以@@符号开头
初始化 |	不需要初始化，未初始化的局部变量被解释为没有参数的方法| 不需要初始化，未初始化的全局变量的值为:nil。| 不需要初始化,未初始化的实例变量的值为:nil。| 需要在使用前进行初始化,未初始化的全局变量会导致错误。



对象是否存在
---

```

nil.to_s  => ""  #对象转化成字符串

nil.to_s.empty?  => true

"foo".nil? => false

nil.nil?  => true


# nil 俩次取反
!!nil	=> false

除此之外，其他所有 Ruby 对象都是“真”值，数字 0 也是：

!!0	=> true


```


### 函数定义

```

>> def string_message(str = '')
>>   if str.empty?
>>     "It's an empty string!"
>>   else
>>     "The string is nonempty."
>>   end
>> end
>> 

# Ruby 方法不用显式指定返回值，方法的返回值是最后一个语句的计算结果

>> def string_message(str = '')
>>   return "It's an empty string!" if str.empty?
>>   return "The string is nonempty."
>> end
>> 

```


###  面向对象

```

> str.class
 => String 

> str.class.superclass
 => Object 
 
> str.class.superclass.superclass
 => BasicObject 
 
> str.class.superclass.superclass.superclass
 => nil 

```


### 类方法

```

  # 类方法 定义1
  def self.info
    "this is a circle class"
  end

  # 类方法 定义2
  class << self
    def infos
      "This is a circle infos class"
    end

    def demo
      "This is a demo"
    end
  end
  

```

### 模块的定义

```

module Forest
  class Rock ; end
  class Tree ; end
  class Animal ; end

end

p Forest::Tree.new
p Forest::Rock.new

```

### 混合类

```


module Device
  def switch_on;
    puts "on"
  end

  def switch_off;
    puts "off"
  end
end

module Volume
  def volume_on;
    puts "on"
  end

  def volume_off;
    puts "off"
  end
end

module Pluggable
  def plug_in;
    puts "in"
  end
  def plug_out;
    puts "out"
  end
end

class CellPhone
  include Device, Volume, Pluggable

  def ring
    puts "ringing"
  end
end

cellPhone = CellPhone.new
cellPhone.switch_on
cellPhone.volume_on
cellPhone.ring


```

### 异常使用

```

begin
  if age < 18
    raise "Person is a minor"
  end
  puts "Entry allowed"
rescue => e
  puts e
end


```