
##### get() , getQueryParams() 和 getQueryParam() 用于获取查询参数：

- get() 用于获取GET参数，可以指定所要获取的特定参数的参数名，在这个参数名不存在时，可以指定默认值。 当不指定参数名时，获取所有的GET参数。 具体功能是由下面2个函数来实现的。
- getQueryParams() 用于获取所有的GET参数。 这些参数的内容，保存在 $_GET 或 $this->_queryParams 中。优先使用 $this->_queryParams 的。
- getQueryParam() 对应于 get() 用于获取特定的GET参数的情况。
而 post() , getPostParams() 和 getPostParam() 用于获取POST参数：

##### post() 与 get() 类似，可以指定所要获取的特定参数的参数名，在这个参数名不存在时，可以指定默认值。 当不指定参数名时，获取所有的POST参数。 具体功能是由下面2个函数来实现的。
- getPostParam() 用于通过参数名获取特定的POST参数，需要调用 
- getPostParams() 获取所有的POST参数。
- getPostParams() 用于获取所有的POST参数。