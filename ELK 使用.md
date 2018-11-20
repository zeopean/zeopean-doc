## mac 安装 ELK


### 安装 elasticsearch

```

brew install elasticsearch

brew services start elasticsearch
brew services stop elasticsearch


配置信息：

	Data:    /usr/local/var/lib/elasticsearch/elasticsearch_zeopean/
	Logs:    /usr/local/var/log/elasticsearch/elasticsearch_zeopean.log
	Plugins: /usr/local/var/elasticsearch/plugins/
	Config:  /usr/local/etc/elasticsearch/

```


### 安装 logstash

```

brew install logstash

启动：

	bin/logstash -e 'input { stdin { } } output { stdout {} }'



```
