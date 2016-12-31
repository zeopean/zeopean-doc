

## docker 容器的几本操作

```
    docker run -it --name   交互的容器终端
    docker ps -a -l         查看容器
    docker inspect          查看容器详细信息
    docker start -i         启动容器
    docker rm               删除容器

```


### 查看docker 运行状态

#### docker日志
```
    docker logs [-f][-t][--tail] 容器名
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


## docker 镜像

### 镜像的操作

#### docker images      列出镜像

