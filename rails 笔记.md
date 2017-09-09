代码自动生成
---

```
rails generate scaffold Micropost content:text user_id:integer
```

模型使用
---

创建（删除）模型

```

rails generate model User name:string email:string 

rails destroy model User

```

* 值域的结束值使用 -1 时，不用知道数组的长度就能从起始值开始一直获取到最后一个元素：

```

>> a = (0..9).to_a
=> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>> a[2..(a.length-1)]               # 显式使用数组的长度
=> [2, 3, 4, 5, 6, 7, 8, 9]
>> a[2..-1]                         # 小技巧，索引使用 -1
=> [2, 3, 4, 5, 6, 7, 8, 9]

```



数据迁移（回滚）

```

rails db:migrate VERSION=0

rails db:rollback


(bandle 版)
bundle exec rake db:migrate

```


进入console
---

```
rails console

```

生成(删除)控制器
---

```

rails generate controller StaticPages home help


rails destroy  controller StaticPages home help


```

### rails简写

```

一些 Rails 命令的简写形式	| 完整形式	简写形式
$ rails server		$ rails s
$ rails console		$ rails c
$ rails generate		$ rails g
$ rails test			$ rails t
$ bundle install		$ bundle


```
