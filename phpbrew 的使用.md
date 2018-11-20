
- phpbrew variants

default的参数：

default: bcmath, bz2, calendar, cli, ctype, dom, fileinfo, filter, ipc,   json, mbregex, mbstring, mhash, mcrypt, pcntl, pcre, pdo, phar, posix,   readline, sockets, tokenizer, xml, curl, openssl, zip


- 使用和切换
- 临时使用:

```

phpbrew use php-5.6.30

```

- 切换版本(设置默认版本):

```
phpbrew switch php-5.6.30

```

- 关闭:

```
phpbrew off

```

- 显示已经安装过的PHP版本

```
phpbrew list

```

- 管理FPM
  NGINX需要配合php-fpm使用,因此,如果是使用 LNMP 或者自己安装的NGINX+PHP的运行环境,则需要在phpbrew安装PHP的时候加上+fpm 模块,才能使用phpbrew的模块管理.

启动FPM:

```

phpbrew fpm start

```

停止FPM

```
phpbrew fpm stop

```

显示php-fpm的模块:

```
phpbrew fpm module

```

测试php-fpm的配置

```
phpbrew fpm test

```

配置php-fpm

```
phpbrew fpm config

```
