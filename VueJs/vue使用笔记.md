1.vue使用jquery

```

	global.jquery = require('jquery')
	var $ = global.jquery
	window.$ = $
	$(function () {
	  $('#app').html('zeopean hello')
	})
	
```

2.错误 Many incorrect "Strings must use singlequote" errors 解决方法
```

修改.eslintrc.js

加上 "quotes": [2, "single", {"avoidEscape": true, "allowTemplateLiterals": true}]

```