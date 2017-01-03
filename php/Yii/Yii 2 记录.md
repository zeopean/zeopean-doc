// 载自  Yii2.0开发qq群： 304864863

最近工作中需要使用YII，下边是学习时顺便记录下的流水账：希望对初学者有些帮助
Active Record (AR) 是一个流行的 对象-关系映射 (ORM) 技术。 每个 AR 类代表一个数据表（或视图），数据表（或视图）的列在 AR 类中体现为类的属性，一个 AR 实例则表示表中的一行。 常见的 CRUD 操作作为 AR 的方法实现。因此，我们可以以一种更加面向对象的方式访问数据。 例如，我们可以使用以下代码向 tbl_post 表中插入一个新行。

        
        $post=new Post;
        $post->title='sample post';
        $post->content='post body content';
        $post->save();

		$User = User::model();
		$User->setIsNewRecord(true);//设置记录是不是是新的
		$User->name='wangliweid';
		$User->sex=1;
		$User->insert();	//添加
		
		$User = new User;  //添加的时候才可以是new 其他的都是 user::model();
		$User->name='wangdsdfliweid';
		$User->insert();	
		
		$User = User::model()->findByPk(1);//根据ID修改 先是获取id然后知道其内容进行修改
		$User->name='wangliwei';
		$User->sex=1;
		$User->save();

		//这是model层 连接数据库 制定数据库
		public function tableName()
        {
            return '{{post}}'; //使用表前缀功能
        }
        //根据某个ID进行删除
        $post=Post::model()->findByPk(10); // 假设有一个帖子，其 ID 为 10
        $post->delete(); // 从数据表中删除此行
    
AR 依靠表中良好定义的主键。如果一个表没有主键，则必须在相应的 AR 类中通过如下方式覆盖 primaryKey() 方法指定哪一列或哪几列作为主键。


    public function primaryKey()
    {
        return 'id';
        // 对于复合主键，要返回一个类似如下的数组
        // return array('pk1', 'pk2');
    }

**3. 创建记录** 
要向数据表中插入新行，我们要创建一个相应 AR 类的实例，设置其与表的列相关的属性，然后调用 save() 方法完成插入：

    $post=new Post;
    $post->title='sample post';
    $post->content='content for the sample post';
    $post->create_time=time();
    $post->save();


记录在保存（插入或更新）到数据库之前，其属性可以赋值为 CDbExpression 类型。 例如，为保存一个由 MySQL 的 NOW() 函数返回的时间戳，我们可以使用如下代码

    $post=new Post;
    $post->create_time=new CDbExpression('NOW()');
    // $post->create_time='NOW()'; 不会起作用，因为
    // 'NOW()' 将会被作为一个字符串处理。
    $post->save();
    
提示: 由于 AR 允许我们无需写一大堆 SQL 语句就能执行数据库操作， 我们经常会想知道 AR 在背后到底执行了什么 SQL 语句。这可以通过开启 Yii 的 日志功能 实现。例如，我们在应用配置中开启了 CWebLogRoute ，我们将会在每个网页的最后看到执行过的 SQL 语句。

**4. 读取记录 **
要读取数据表中的数据，我们可以通过如下方式调用 find 系列方法中的一种：

    // 查找满足指定条件的结果中的第一行
    $post=Post::model()->find($condition,$params);
    
    例子1：
    $post=Post::model()->find($condition,$params);  
    $post=Post::model()->find('postID=:postID', array(':postID'=>10)); 
    
    例子2：
    $criteria=new CDbCriteria;
    $criteria->select='title';
    $criteria->condition='postID=:postID';
    $criteria->params=array(':postID'=>10);
    $post=Post::model()->find($criteria); // $params 不需要了
    
注意，当使用 CDbCriteria 作为查询条件时，$params 参数不再需要了，因为它可以在 CDbCriteria 中指定，就像上面那样

一种替代 CDbCriteria 的方法是给 find 方法传递一个数组。 数组的键和值各自对应标准（criterion）的属性名和值，上面的例子可以重写为如下：

    $post=Post::model()->find(array(
        'select'=>'title',
        'condition'=>'postID=:postID',
        'params'=>array(':postID'=>10),
    ));

// 查找具有指定主键值的那一行

    $post=Post::model()->findByPk($postID,$condition,$params);
    例子1:
    $post=Post::model()->find(array(  
        'select'=>'title',  
        'condition'=>'postID=:postID',  
        'params'=>array(':postID'=>10),  
    ));  
    $post=Post::model()->findByPk($postID,$condition,$params);  
    
// 查找具有指定属性值的行

    $post=Post::model()->findByAttributes($attributes,$condition,$params);
    //例子1：
    $checkuser = user_field_data::model()->findByAttributes(  
        array('user_id' => Yii::app()->user->user_id, 'field_id' => $fieldid));  
    //例子2：
    $user_field_data = user_field_data::model()->findAllByAttributes(  
        $attributes = array('user_id' => ':user_id'),  
        $condition = "field_id in (:fields)",  
        $params = array(':user_id' => Yii::app()->user->user_id, ':fields' => "$rule->dep_fields")); 
        
// 通过指定的 SQL 语句查找结果中的第一行

    $post=Post::model()->findBySql($sql,$params);
    
    // 获取满足指定条件的行数
    $n=Post::model()->count($condition,$params);
    // 通过指定的 SQL 获取结果行数
    $n=Post::model()->countBySql($sql,$params);
    // 检查是否至少有一行复合指定的条件
    $exists=Post::model()->exists($condition,$params);

直接更新数据表中的一行或多行而不首先载入也是可行的。 AR 提供了如下方便的类级别方法实现此目的：

// 更新符合指定条件的行

    Post::model()->updateAll($attributes,$condition,$params);
// 更新符合指定条件和主键的行

    Post::model()->updateByPk($pk,$attributes,$condition,$params);
// 更新满足指定条件的行的计数列
    
    Post::model()->updateCounters($counters,$condition,$params);
    
在上面的代码中， $attributes 是一个含有以 列名作索引的列值的数组； $counters 是一个由列名索引的可增加的值的数组；$condition 和 $params 在前面的段落中已有描述。

如果一个 AR 实例被一行数据填充,我们也可以删除此行数据。

    $post=Post::model()->findByPk(10); // 假设有一个帖子，其 ID 为 10
    $post->delete(); // 从数据表中删除此行
注意，删除之后， AR 实例仍然不变，但数据表中相应的行已经没了。

使用下面的类级别代码，可以无需首先加载行就可以删除它。

    // 删除符合指定条件的行
    Post::model()->deleteAll($condition,$params);
    // 删除符合指定条件和主键的行
    Post::model()->deleteByPk($pk,$condition,$params);



当调用 save() 时， AR 会自动执行数据验证。 验证是基于在 AR 类的 rules() 方法中指定的规则进行的。 关于验证规则的更多详情，请参考 声明验证规则 一节。 下面是保存记录时所需的典型的工作流。

    if($post->save())
    {
        // 数据有效且成功插入/更新
    }
    else
    {
        // 数据无效，调用  getErrors() 提取错误信息
    }
当要插入或更新的数据由最终用户在一个 HTML 表单中提交时，我们需要将其赋给相应的 AR 属性。 我们可以通过类似如下的方式实现：

    $post->title=$_POST['title'];
    $post->content=$_POST['content'];
    $post->save();

如果有很多列，我们可以看到一个用于这种复制的很长的列表。 这可以通过使用如下所示的 attributes 属性简化操作。 更多信息可以在 安全的特性赋值 一节和 创建动作 一节找到。

    // 假设 $_POST['Post'] 是一个以列名索引列值为值的数组
    $post->attributes=$_POST['Post'];
    $post->save();


CActiveRecord 提供了几个占位符方法，它们可以在子类中被覆盖以自定义其工作流。

    beforeValidate 
    beforeSave 和 afterSave: 这两个将在保存 AR 实例之前和之后被调用。
    beforeDelete 和 afterDelete: 这两个将在一个 AR 实例被删除之前和之后被调用。
    afterConstruct: 这个将在每个使用 new 操作符创建 AR 实例后被调用。
    beforeFind: 这个将在一个 AR 查找器被用于执行查询（例如 find(), findAll()）之前被调用。 1.0.9 版本开始可用。
    afterFind: 这个将在每个 AR 实例作为一个查询结果创建时被调用。

10. 使用 AR 处理事务 
每个 AR 实例都含有一个属性名叫 ***dbConnection*** ，是一个 CDbConnection 的实例，这样我们可以在需要时配合 AR 使用由 Yii DAO 提供的 事务 功能:
    
        $model=Post::model();
        $transaction=$model->dbConnection->beginTransaction();
        try
        {
            // 查找和保存是可能由另一个请求干预的两个步骤
            // 这样我们使用一个事务以确保其一致性和完整性
            $post=$model->findByPk(10);
            $post->title='new post title';
            $post->save();
            $transaction->commit();
        }
        catch(Exception $e)
        {
            $transaction->rollBack();
        }
        
        $url=$this->createUrl($route,$params);

$this指的是控制器实例; $route指定请求的route 的要求;$params 列出了附加在网址中的GET参数。

默认情况下，URL以get格式使用createUrl 创建。例如，提供$route='post/read'和$params=array('id'=>100) ，我们将获得以下网址：

        /index.php?r=post/read&id=100

除了正常的数据检索和处理查询,查询构建器还提供了一组方法构建和执行SQL查询,可以操纵数据库的模式。特别是,它支持以下查询:

        createTable(): creates a table
        renameTable(): renames a table
        dropTable(): drops a table
        truncateTable(): truncates a table
        addColumn(): adds a table column
        renameColumn(): renames a table column
        alterColumn(): alters a table column
        dropColumn(): drops a table column
        createIndex(): creates an index
        dropIndex(): drops an index

如果浏览器重定位到登录页面，而且登录成功，我们将重定位浏览器到引起验证失败的页面。我们怎么知道这个值呢？我们可以通过用户部件的returnUrl 属性获得。我们因此可以用如下执行重定向：

    Yii::app()->request->redirect(Yii::app()->user->returnUrl);
    
    $this->preinit();
    $this->init();

    #self::$classMap 可以在这里定义类的路径，在autoload里调用

//页面缓存控制器入口
可在main.php 中  设置catchAllRequest
	
	$route=$this->catchAllRequest[0];

CModule 重载了 Ccomponent 的__get 方法

Yii::setApplication($this); 将app设置为了application对象

先注册component,这时并没有加载他们，只有在getcomponet时才加载。

 

**设置cookie**

    $cookie = new CHttpCookie('mycookie','this is my cookie');
    $cookie->expire = time()+60*60*24*30;  #有限期30天
    Yii::app()->request->cookies['mycookie']=$cookie;
    
    #这里的cookies 继承了CCookieCollection ，他是CMap类型,重写了add等等，在add中设置了cookie.
    #比如$cookie = Yii::app()->request->cookies;
    $cookies['name'] = $cookie;
   
    #读取cookie:
    $cookie = Yii::app()->request->getCookies();
    echo $cookie['mycookie']->value;
    
    #销毁cookie:
    $cookie = Yii::app()->request->getCookies();
    unset($cookie[$name]);




**过滤器**
	
	public function filterAccessAuth($filterChain) {  
		echo 'a';
		$filterChain->run();
	}
	
	public function filterAbc($filterChain) {  
		$filterChain->run();
	}
	public function filters() {  
        return array(  
            'accessAuth  + session',  
			'abc',
        );  
    }




**分页：**

    #Controller action:
    function actionIndex(){
        $criteria=new CDbCriteria();
        $count=Article::model()->count($criteria);
        $pages=new CPagination($count);
    
        // results per page
        $pages->pageSize=10;
        $pages->applyLimit($criteria);
        $models=Article::model()->findAll($criteria);
    
        $this->render('index', array(
        'models' => $models,
             'pages' => $pages
        ));
    }


    #View:
    <?php foreach($models as $model): ?>
        // display a model
    <?php endforeach; ?>
    
    // display pagination
    <?php $this->widget('CLinkPager', array(
        'pages' => $pages,
    )) ?>




