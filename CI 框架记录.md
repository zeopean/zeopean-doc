## composer 添加本地目录

```

需要在 composer.json 文件中添加 一下配置：

	"autoload": {
		"classmap": [
			"p_application/admin","p_application/home"
		],
		"psr-4": {
			"Admin\\": "p_application/admin",
			"Home\\": "p_application/home"
		}
	}

```


## ci 视图类中使用 变量


```

 // 控制器
 $this->load->vars('account', []);


 // 视图
 $account = $this->load->get_var('account');




```