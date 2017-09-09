### ubuntu 镜像地址更新

```


使用vi的替换方法： 
vi /etc/apt/sources.list 

打开之后依次输入以下命令：
(正则替换，也可以手动将 http://archive.ubuntu.com 改为 http://cn.archive.ubuntu.com)

:%s/us.archive/cn.archive/g 


```