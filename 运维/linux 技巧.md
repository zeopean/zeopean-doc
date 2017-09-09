

#### 文件传输

```

scp ~/Desktop/excel.zip   common@121.41.30.169:/home/www/box4_home/ceping-wz/wx/pub/New/data

```



#### rz,sz的使用

- 软件安装

```
首先通过sftp工具把安 装文件上传到/tmp目录下.

# cd /tmp

# wget http://down1.chinaunix.net/distfiles/lrzsz-0.12.20.tar.gz

# tar zxvf lrzsz-0.12.20.tar.gz && cd lrzsz-0.12.20

# ./configure && make && make install


上面安装过程默认把lsz和lrz安装到了/usr/local/bin/目录下, 下面创建软链接, 并命名为rz/sz:

# ln -s /usr/local/bin/lrz /usr/bin/rz

# ln -s /usr/local/bin/lsz /usr/bin/sz

```