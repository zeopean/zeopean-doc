
    <?php
    abstract class Obj   
    {  
            private $objData        = array();  
            /**  
             * __call魔术方法，如果对象请求的方法不存在或者没有权限访问的时候 
             * 调用魔术方法 
             */  
            public function __call($name, $args) {  
                $field = preg_match('/^get(\w+)/', $name, $matches);  
                if ( $field && $matches[1] )  
                    return $this->objData[strtolower($matches[1])];  
                $field = preg_match('/^set(\w+)/', $name, $matches);  
                if ( $field && $matches[1] ) {   
                    return $this->objData[strtolower($matches[1])] = $args[0];  
                }     
            }     
    
            public static function __callStatic($name, $args) {  
                $field = preg_match('/^get(\w+)/', $name, $matches);  
                if ( $field && $matches[1] )  
                    return self::$objData[strtolower($matches[1])];  
                $field = preg_match('/^set(\w+)/', $name, $matches);  
                if ( $field && $matches[1] ) {   
                    return self::$objData[strtolower($matches[1])] = $args[0];  
            }     
        } 
    
    
    } 