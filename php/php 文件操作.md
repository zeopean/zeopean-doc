 
#### 文件操作
广义的文件：计算机中任何可以看到的数据，其中文件夹是特殊的文件
狭义的文件：计算机中除了路径（文件夹）之外的所有数据
 
文件操作包含两种：路径操作（文件夹）和文件操作
 
#### 路径操作
路径操作即文件夹操作：创建和删除，重命名等，通过文件夹得到其内部的文件。
 
#### 访问文件夹

    - opendir：打开路径，返回一个路径资源
    
    - readdir：从路径资源中去读取文件信息，一次只能读取一个，读取的是文件的名字，资源指针会下移（读
     
    
    - closedir：关闭资源



#### 路径操作函数

    - rewinddir：rewind与reset一样，是重置的意思：将资源指针指向第一个文件
    
    
    - scandir：scan是浏览的意思，能够直接读取一个路径下面所有文件。（不需要打开文件资源）
     
    
    - file_exists：判断文件是否存在（路径也可以判断）
    
    
    - is_dir：判断是否是一个路径
    
    
    - is_file：判断是否是一个文件
    
    
    - mkdir：创建文件夹
    
    
    - rmdir：删除文件夹
    
    
    - getcwd：获取当前工作目录
    
    
    - chdir：改变当前工作目录


- 修改工作目录的应用
```
<?php
$dir = ‘./’;
chdir(‘../‘) ; //改变路径
$o = opendir($dir);  //路径操作
while($file = readdir($o)){  //循环遍历数组
   echo $file,’<br/>’;  //输出文件名
       }
closedir($o);
```

- 自定义scandir函数  function myScandir($dir)
```
<?php
    header(‘content-type:text/html;charset=utf-8’);
    function myScandir($dir){
    $file = Opendir($dir);  //打开文件目录
    while($filename = readdir($file)){
    $filename = iconv(‘GBK’, ‘UTF-8’, $filename);
    $files[] = $filename;   //把遍历来的数据存档到数组中
    }
    return $files;  //返回数组
    }
```


#### 文件操作

    - file_get_contents：从指定文件中获取整个数据，返回一个字符串
     
    - file_put_contents：至少需要两个参数，要写入的字符串，写到哪个文件,如果要写入的目标文件不存在，系统会自动创建。
    
    - fopen：打开文件获得该文件的资源，文件的打开必须指定模式
    
    - fgetc：c代表character，字符，一次读取一个字符，读完之后指针下移
    
    - fgets：s代表string，读取多个字符，可以指定字符长度，也可以不指定，不指定的情况下默认的是读取一行（最多读取一行）
    
    - fread：读取指定长度的数据，默认读取长度8192 个字节（最多）
    
    - fwrite/fputs：将指定字符串写入到文件当前指针所在位置，返回的结果是写入成功的字节数
    
    - fclose：关闭对应的资源
     
    - fseek: 文件资源指针移动
    
    - copy：复制，会保留原文件，只是新生成一份
     
    - unlink：断开关联，删除文件
     
    - rename：重命名文件
    
    - filemtime：m代表modify，修改，得到文件最后被修改的时间
     
    - filesize：文件的大小，结果是以字节为单位
     
    - fileperms：文件的权限关系
 


 