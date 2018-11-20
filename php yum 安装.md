
## 安装 php 扩展

```
sudo yum install php72


sudo yum install -y php72-php-devel  php72-php-fpm  php72-php-mbstring php72-php-memcache php72-php-redis  php72-php-mysqli php72-php-mysqlnd  php72-php-pdo  php72-php-bcmath php72-php-dom php72-php-gd php72-php-gmp php72-php-igbinary php72-php-imagick   php72-php-mcrypt  php72-php-pdo_mysql php72-php-posix php72-php-simplexml  php72-php-opcache php72-php-xsl php72-php-xmlwriter php72-php-xmlreader php72-php-xml php72-php-swoole php72-php-zip


```


## 设置开机自启

```
$ sudo systemctl enable php72-php-fpm.service

```

## 常用 php-fpm 命令

```

- 开启服务
$ sudo systemctl start php72-php-fpm.service

- 停止服务
$ sudo systemctl stop php72-php-fpm.service

- 查看状态
$ sudo systemctl status php72-php-fpm.service

```

