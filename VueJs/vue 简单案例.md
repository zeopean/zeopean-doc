
1.安装 vue
```
    npm install vue -g --registry=https://registry.npm.taobao.org
    
    npm install vue-cli --global --registry=https://registry.npm.taobao.org

```

2.配置vue
```
#创建vue软链接
    ln -s /usr/local/Cellar/node/5.9.0/libexec/npm/lib/node_modules/vue-cli/bin/vue /usr/local/bin/vue
    
#创建vue-init 软链接
    ln -s /usr/local/Cellar/node/5.9.0/libexec/npm/lib/node_modules/vue-cli/bin/vue-init /usr/local/bin/vue-init
```

3.创建项目app1
```
    vue init webpack app1
```
- 已经安装啦webpack，可参考 http://www.cnblogs.com/zeopean/p/webpack.html

4.根据提示进行 npm install 操作
```
    npm install --registry=https://registry.npm.taobao.org
```

5.vue使用jquery

```

	global.jquery = require('jquery')
	var $ = global.jquery
	window.$ = $
	$(function () {
	  $('#app').html('zeopean hello')
	})
	
```





## 错误 Many incorrect "Strings must use singlequote" errors 解决方法
```

修改.eslintrc.js

加上 "quotes": [2, "single", {"avoidEscape": true, "allowTemplateLiterals": true}]

```