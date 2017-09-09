
### nginx命令

```
kill -HUP pid 		从容地重启nginx


```


### nginx 编译参数
```

./configure \
--prefix=/usr/local/nginx \
--sbin-path=/usr/local/nginx/sbin/nginx \
--conf-path=/usr/local/nginx/conf/nginx.conf \
--pid-path=/usr/local/nginx/logs/nginx.pid \
--lock-path=/usr/local/nginx/lock/nginx.lock \
--error-log-path=/usr/local/nginx/logs/error.log \
--http-log-path=/usr/local/nginx/logs/access.log \
--http-scgi-temp-path=/usr/local/nginx/scgi \
--http-uwsgi-temp-path=/usr/local/nginx/uwsgi \
--http-proxy-temp-path=/usr/local/nginx/proxy \
--http-fastcgi-temp-path=/usr/local/nginx/fastcig \
--http-client-body-temp-path=/usr/local/nginx/body \
--user=www-data \
--group=www-data \
--with-ipv6 \
--with-debug \
--with-file-aio \
--with-http_ssl_module \
--with-http_flv_module \
--with-http_mp4_module \
--with-http_sub_module \
--with-http_dav_module \
--with-http_xslt_module \
--with-http_geoip_module \
--with-http_realip_module \
--with-http_addition_module \
--with-http_gzip_static_module \
--with-http_secure_link_module \
--with-http_degradation_module \
--with-http_stub_status_module \
--with-http_random_index_module \
--with-http_image_filter_module

```