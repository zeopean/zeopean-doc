
参考地址：
http://www.kancloud.cn/manual/yii2-guide/69701

* 启用／停止／销毁


    $session = Yii::$app->session;

    // 检查session是否开启 
    if ($session->isActive) ...
    
    // 开启session
    $session->open();
    
    // 关闭session
    $session->close();
    
    // 销毁session中所有已注册的数据
    $session->destroy();