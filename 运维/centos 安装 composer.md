
* 下载安装包
    
        curl -sS https://getcomposer.org/installer | php

* 把 composer 把复制到  /usr/bin/composer
    
        mv composer.phar /usr/bin/composer

* composer 运行，ok

* caomposer 报错，以及解决方法

        Failed to decode response: zlib_decode(): data error
        Retrying with degraded mode, check https://getcomposer.org/doc/articles/troubleshooting.md#degraded-mode for more info
        
解决方法是：
    composer -vvv update
