

- 参考：
    
    http://www.jianshu.com/p/c28e5df8647d
    http://www.jianshu.com/p/397df5dfd09c
    
1.该案例的目录结果如下
```
zpvue
    app
        main.js
        module1.js
        module2.js
    public
        bundle.js
        index.html
    package.json
    webpack.config.js
```

2.安装 webpack
```
    npm install webpack --save-dev --registry=https://registry.npm.taobao.org

```
##### 使用以下命令进行webpack 初始化
```
npm init
```

##### 配置webpack.json文件
```
{
  "name": "zpvue",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start":"webpack -p"    //对应5.webpack 的命令
  },
  "author": "zeopean",
  "license": "ISC",
  "devDependencies": {
    "css-loader": "^0.26.0",
    "extract-text-webpack-plugin": "^1.0.1",
    "sass-loader": "^4.0.2",
    "style-loader": "^0.13.1",
    "webpack": "^1.13.3"
  }
}


```
- scripts:start 明亮对应 ＝>5.webpack 的命令
- scripts.devDependencies 在3.安装加载器时会主动添加

3.安装loader 加载器
```
    npm install sass-loader style-loader css-loader extract-text-webpack-plugin --save-dev --registry=https://registry.npm.taobao.org

```

4.配置webpack.config.js 文件
```
/**
 * Created by zeopean on 16/11/19.
 */
var webpack = require('webpack')
var ExtractTextPlugin = require("extract-text-webpack-plugin");
module.exports = {
    //页面入口
    entry:{
        index:  './app/main.js'
    },
    //入口文件输出配置
    output:{
        path:'./public',
        filename:'bundle.js'
    },
    //加载模块
    module:{
        loaders:[{
            test:'/\.sass$/',
            loader:ExtractTextPlugin.extract('style-loader', 'css-loader!sass-loader')
        }]
    },
    plugins:[
        new ExtractTextPlugin('[name].css')
    ]
};


```
    
- entry 表示入口
- output 表示输出打包后的bundle.js
- module表示加载器


5.webpack 的命令
```
关于webpack的启动方式：

webpack         // 最基本的启动webpack的方法

webpack -w      // 提供watch方法；实时进行打包更新

webpack -p      // 对打包后的文件进行压缩

webpack -d      // 提供source map，方便调式代码




```

6.引入输出的bundle.js
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>webpack demo</title>
</head>
<body>

</body>
<script type="text/javascript" src="../public/bundle.js"></script>
</html>

```