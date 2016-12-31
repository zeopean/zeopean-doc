下面简单介绍下关于yii2 的数据库操作语句，需要注意的关键词有

    createCommand   -- 参数可以是sql语句
    queryAll        -- 查询所有的数据
    queryOne        -- 获取单条数据
    queryScalar     -- 获取总数
    execute         -- 执行sql语句
    insert          -- 插入操作
    batchInsert     -- 插入多条数据
    delete          -- 删除操作
    bindValue       -- 绑定参数
    bindParam       -- 绑定引用参数
    
        


* 数据库操作

        public function actionOptions()
        {
            $conn = \Yii::$app->db;
    
            ＃对于查询语句,使用  query 系列方法
            /*获取所有数据*/
            $command = $conn->createCommand("select * from country");
            $countries = $command->queryAll();
            //        var_dump($countries);
    
            /*获取单条数据*/
            $command = $conn->createCommand("select * from country where code='AU'");
            $country = $command->queryOne();
            //        var_dump($country);
    
            /*返回列数据*/
            $command = $conn->createCommand("select code from country ");
            $code    = $command->queryColumn();
            //        var_dump($code);
    
            /*返回统计数*/
            $command = $conn->createCommand("select count(*) from country");
            $counts  = $command->queryScalar();
            //        echo $counts;
    
    
            ＃对于非查询语句,使用  execute
            ＃更新操作
                $command = $conn->createCommand("update country set name='澳大利亚' where code ='AU'");
            $command->execute();
    
        //        插入操作 单条插入
        //        $conn->createCommand()->insert('country' , [
        //            'code'  => 'Y23',
        //            'name'  => '燕山',
        //            'population' => '12122'
        //        ])->execute();
            ＃多条插入
            $conn->createCommand()->batchInsert('country' , ['code' , 'name' , 'population'] , [
                [
                    'U2',
                    '颜色',
                    '12122'
                ],
    
            ])->execute();
        
            ＃删除数据
            $conn->createCommand()->delete('country' , 'code="YY"')->execute();
    
        }
        
        

* 参数绑定操作
    
        public function actionActive()
        {
            $conn = \Yii::$app->db;
            ＃ 预申明查询  bindValue 的使用
            $command = $conn -> createCommand("select * from country where code=:code");
            $command->bindValue(':code' , 'US');
            $country = $command->queryOne();
            //        var_dump($country);
        
            ＃ 预备声明 bindParam  的使用
            $command = $conn->createCommand("select * from country where code =:code");
            $command->bindParam(':code' , $code);

            $code ='US';
            $command->execute();
            $country = $command->queryOne();
            var_dump($country);
            echo '<br>';
    
            $code = 'AU';
            $command->execute();
            $country = $command->queryOne();
            var_dump($country);

    }
    
    
* yii 查询生成器
    
        [[yii\db\Query::all()|all()]]: 生成和执行查询并返回数组形式的所有查询结果。
        [[yii\db\Query::one()|one()]]: 返回结果集的第一行。
        [[yii\db\Query::column()|column()]]: 返回结果集的第一列。
        [[yii\db\Query::scalar()|scalar()]]: 返回结果集第一行的第一列
        [[yii\db\Query::exists()|exists()]]: 返回指明查询结果是否存在的值。
        [[yii\db\Query::count()|count()]]: 返回 COUNT 查询的结果。其他相似的方法包括 sum(), average(), max(), min(), 这些方法支持所谓数据的聚集查询。


* 关键字

        select      -- 要查询的字段
        from        -- 要查询的表
        offset      -- 从第几条纪录开始
        limit       -- 取多少条数据
        orderBy     -- 排序
        where       -- where 条件的使用
        appParam    -- where 查询绑定参数
        andWhere    -- where 中 and 的使用
        orWhere     -- where 中 or 的使用
        join        -- 表连接查询
        leftJoin    -- 左连接
        rightJoin   -- 右连接
        innerJoin   -- 内连接

* 案例

        $rows = (new \yii\db\Query())->select('code , name')->from('country')->limit(10)->offset(2)->orederBy('name')->all();
        
        


