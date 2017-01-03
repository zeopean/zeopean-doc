#### 创建数据库

```
#在 parameters.yml 配置数据库参数
parameters:
    database_host: localhost
    database_port: 6379
    database_name: symfony3
    database_user: admin
    database_password: admin
    mailer_transport: smtp
    mailer_host: smtp.163.com
    mailer_user: zeopean@163.com
    mailer_password: ***
    secret: 36efc1643d2c2efade682c27ac102d564ff1f421
    
#配置config.yml
doctrine:
    dbal:
        driver:   pdo_mysql
        host:     "%database_host%"
        port:     "%database_port%"
        dbname:   "%database_name%"
        user:     "%database_user%"
        password: "%database_password%"
        charset:  UTF8


php console doctrine:database:create 

```