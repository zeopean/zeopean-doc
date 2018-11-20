### bee 安装

```

go get github.com/beego/bee


```

### 拉取beego 包

```
go get github.com/astaxie/beego 

```

### 创建新web 项目

```
bee new beegoApp

```


### 创建api 项目

```

bee api beegoApi

```

### 查看bee 版本

```

bee version

```

### bee 代码生成

```

bee generate model [modelname] [-fields=""]  模型

bee generate controller [controllerfile] 控制器

bee generate view [viewpath] 视图

bee generate migration [migrationfile] [-fields=""] 数据迁移
    
bee generate docs
    
bee generate test [routerfile] 测试文件


```