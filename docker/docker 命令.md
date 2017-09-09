







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


## docker 镜像

### 镜像的操作

#### docker images      列出镜像

