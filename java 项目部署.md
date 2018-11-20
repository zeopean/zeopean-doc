## 运行部署

```

nohup java -jar target/guns-rest-0.0.1-SNAPSHOT.jar --spring.config.location=application-prod.yml &

nohup java -jar target/guns-admin.jar --spring.config.location=application-prod.yml &

```


## 构建出生产环境需要的war包
```

mvn clean package -Ppro


```

## 文件传输

```

 scp /Users/zeopean/Desktop/214833639380687.zip  root@118.31.62.207:/tmp

```