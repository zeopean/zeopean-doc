

### 使用163 docker仓库
```

docker pull hub.c.163.com/public/ubuntu:14.04

```

### docker-composer

```



```



### 删除所有未运行的镜像和容器
```
docker rm (docker ps -q -f status=exited)  

```

### 删除所有的镜像和容器

```
docker kill (docker ps -q) ; docker rm (docker ps -a -q) ; docker rmi (docker images -q -a)

```

### 保存镜像容器
```

docker commit -m "ubuntu 14.04 test " 7828a5d511ce(正再运行的) ubuntu:14.04 

```

### docker 信息
```

docker -D info 

```



## boot2docker

```
boot2docker ssh   ssh 登录
boot2docker ip 	 查看ip地址
boot2docker init  初始化
boot2docker start 启动
boot2docker status 查看状态



```







## docker 容器的几本操作

```
    docker run -it --name   	交互的容器终端
    docker ps -a -l         	查看容器
    docker inspect ［name］    查看容器详细信息
    docker rm ［name］         删除容器
    docker start [name]     	启动
    docker port [name] 		 	查看端口号

```









### 查看docker 运行状态

#### docker日志
```
    docker logs [-f][-t][--tail] [name]
        -f      
        -t      
        --tail  all

```

#### docker top     类似 top

#### docker stop/kill   docker 容器停止运行
        
#### docker run -d      docker 后台运行      

### 启动容器中的新进程

```
    docker exec [-d][-i][-t] 容器名
```


## docker-machine 

```
docker-machine create -d virtualbox --virtualbox-memory 2048 --virtualbox-disk-size 204800 default

```


### 创建默认docker

```
docker-machine create --driver virtualbox default


```


## docker 镜像

### 镜像的操作

#### docker images      列出镜像

## 搜索可用镜像

目标：
学会使用命令行的工具来检索名字叫做tutorial的镜像。

提示：
命令行的格式为：docker search 镜像名字

```

docker search tutorial 

```

## 拉取镜像

目标：
通过docker命令下载tutorial镜像。

提示：
执行pull命令的时候要写完整的名字，比如"learn/tutorial"。

正确的命令：

```
$docker pull learn/tutorial

```

## 运行

目标：
在我们刚刚下载的镜像中输出"hello word"。为了达到这个目的，我们需要在这个容器中运行"echo"命令，输出"hello word"。

提示：
docker run命令有两个参数，一个是镜像名，一个是要在镜像中运行的命令。

正确的命令：

```
$docker run learn/tutorial echo "hello word"

```

## 在容器中安装应用

目标：
在learn/tutorial镜像里面安装ping程序。

提示：
在执行apt-get 命令的时候，要带上-y参数。如果不指定-y参数的话，apt-get命令会进入交互模式，需要用户输入命令来进行确认，但在docker环境中是无法响应这种交互的。

正确的命令：

```
$docker run learn/tutorial apt-get install -y ping

```

## 保存对容器的修改

目标：
首先使用docker ps -l命令获得安装完ping命令之后容器的id。然后把这个镜像保存为learn/ping。

提示：
1. 运行docker commit，可以查看该命令的参数列表。

2. 你需要指定要提交保存容器的ID。(译者按：通过docker ps -l 命令获得)

3. 无需拷贝完整的id，通常来讲最开始的三至四个字母即可区分。（译者按：非常类似git里面的版本号)

正确的命令：

```
$docker commit 698 learn/ping

```

## 运行新的镜像

目标：
在新的镜像中运行ping www.google.com命令。

提示：
一定要使用新的镜像名learn/ping来运行ping命令。(译者按：最开始下载的learn/tutorial镜像中是没有ping命令的)

正确的命令：

```
$docker run lean/ping ping www.google.com

```

## 检查运行的镜像

目标：
查找某一个运行中容器的id，然后使用docker inspect命令查看容器的信息。

提示：
可以使用镜像id的前面部分，不需要完整的id。

正确的命令：

```
$ docker inspect efe

```

## 登录docker

```

docker login --username=zeopean --email=1412512785@qq.com [zpzeopean759]

```


## 发布镜像

目标：
把learn/ping镜像发布到docker的index网站。

提示：
1. docker images命令可以列出所有安装过的镜像。

2. docker push命令可以将某一个镜像发布到官方网站。

3. 你只能将镜像发布到自己的空间下面。这个模拟器登录的是learn帐号。

预期的命令：


```
$ docker push learn/ping

```


