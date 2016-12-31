
*  设置缓存

        #put 方式
        Cache::put('key', 'value', $minutes);
        
        # 设置文件缓存
        Cache::store('file')->get('foo');

        #使用redis 做缓存
        Cache::store('redis')->put('bar', 'baz', 10);       // 存储在redis 的数据 格式是这样子的，需要注意：1) "laravel:bar"
        
        #其他缓存设置方式
        #add 方法只会把暂时不存在缓存中的项目放入缓存，如果成功存放，会返回 true，否则返回 false：
        
        Cache::add('key', 'value', $minutes);
        
        #forever 方法可以用来存放永久的项目到缓存中，这些值必须被手动的删除，这可以通过 forget 方法实现：

        Cache::forever('key', 'value');
        // 删除使用 Cache::forget('key');
        
* 判断缓存键值是否存在
    
        if(Cache::has('key')){
            # code
        }
            
    

*  获取缓存
        
        ＃获取普通缓存
        $value = Cache::get('foo');
        
        $value = Cache::pull('key');//put 与get 类似
        
        #获取redis 缓存
        $value = Cache::store('redis')->get('bar');

    * 需要注意的是，获取缓存时，可以使用闭包函数的形式
        
            $value = Cache::get('key', function() {
                return DB::table(...)->get();
            });

*  更新缓存
  
    * 有时候，你可能会想从缓存中取出一个项目，但也想在当取出的项目不存在时存入一个默认值，例如，你可能会想从缓存中取出所有用户，当找不到用户时，从数据库中将这些用户取出并放入缓存中，你可以使用 Cache::remember 方法达到目的：
    
            $value = Cache::remember('users', $minutes, function() {
                return DB::table('users')->get();
            });

    * 如果那个项目不存在缓存中，则返回给 remember 方法的闭包将会被运行，而且闭包的运行结果将会被存放在缓存中。
    * 使用 remember 和 forever 这两个方法来 ”永久“ 存储缓存：
    
            $value = Cache::rememberForever('users', function() {
                return DB::table('users')->get();
            });

*  清除缓存 
    
        ＃清除某个缓存
        Cache::forget('key');
    
        # 清除所以缓存
        Cache::flush();
        
        ＃pull 也可以清除缓存，并且获取该值
        Cache::pull('key');



* 键值的递增与递减值(针对整型)
    
    increment 和 decrement 方法可以用来调整缓存中的整数项目值，这两个方法都可以选择性的传入第二个参数，用来指示要递增或递减多少：

        Cache::increment('key');
        
        Cache::increment('key', $amount);
        
        Cache::decrement('key');
        
        Cache::decrement('key', $amount);

