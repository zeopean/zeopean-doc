
### 使用 redis

1. 添加 config/redis.php 配置

```

$config['socket_type'] = 'tcp'; //`tcp` or `unix`
$config['socket'] = '/var/run/redis.sock'; // in case of `unix` socket type
$config['host'] = '127.0.0.1';
$config['password'] = NULL;
$config['port'] = 6379;
$config['timeout'] = 0;


```

2. 使用

```

	    $data = ['name' => 'zeopean'];

	    $this->load->driver('cache');
	    $this->cache->redis->save('data', $data, 100);
	    $tmp = $this->cache->redis->get('data');
	    
```



### session 的设置

1. 更新 config/config.php 的 session 配置

```
$config['sess_driver'] = 'redis';
$config['sess_cookie_name'] = 'ci_session';
$config['sess_expiration'] = 7200;
$config['sess_save_path'] = "tcp://localhost:6379";
$config['sess_match_ip'] = FALSE;
$config['sess_time_to_update'] = 300;
$config['sess_regenerate_destroy'] = FALSE;

```


2. 使用

```

	    $this->load->library('session');
	    $this->session->set_userdata('session_data', $data);
	    $tmp1 = $this->session->userdata('session_data');
	    $this->session->unset_userdata('session_data');


```