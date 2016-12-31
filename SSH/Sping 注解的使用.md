

### import 
    @import 注解允许从 一个配置类中加载 @Bean 定义。
    
    ```java
    
        @Configuration 
        public class ConfigA {
            @Bean public A a() {
            return new A(); }
        }
    ```
    import 后
    ```java
    
    @Configuration 
    @Import(ConfigA.class) 
    public class ConfigB {
        @Bean 
        public B a() {
            return new A(); }
        }
    ```
    
### @Required
    
    @Required 注解应用于 bean 属性的 setter 方法。
    ```java
    package com.spring08;

    import org.springframework.beans.factory.annotation.Required;
    
    /**
     * Created by zeopean on 16/8/22.
     */
    public class Student {
        private String name;
        private Integer age;
    
        public String getName() {
            return name;
        }
        @Required
        public void setName(String name) {
            this.name = name;
        }
    
        public Integer getAge() {
            return age;
        }
        @Required
        public void setAge(Integer age) {
            this.age = age;
        }
    
    }

    
    ```
 
### Aurowired 

    @Autowired 注解可以应用到 bean 属性的 setter 方法,非 setter 方法,构造函数 和属性。
 
### @Qualifier 

    通过指定确切的将被 线的 bean, @Autowired 和 @Qualifier 注解可以用来删除 混乱。
    ```java
    
    package com.spring10;
    
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.beans.factory.annotation.Qualifier;
    
    /**
     * Created by zeopean on 16/8/23.
     */
    public class Profile {
        @Autowired
        @Qualifier("student1")
        private Student student;
    
        public Profile() {
            System.out.println("依赖文件使用中@!");
        }
    
        public void printAge()
        {
            System.out.println("Student Age: " + student.getAge());
        }
    
        public void printName()
        {
            System.out.println("Student Name: " + student.getName());
        }
    }

    
    ```

### @Resource 注解

    ```java
    package com.tutorialspoint; 
    import javax.annotation.Resource;
    
    public class TextEditor {
        private SpellChecker spellChecker;
        
        @Resource(name= "spellChecker")
        public void setSpellChecker( SpellChecker spellChecker ){
            this.spellChecker = spellChecker; 
        }
        
        public SpellChecker getSpellChecker(){ 
            return spellChecker;
        }
        
        public void spellCheck(){
            spellChecker.checkSpelling();
        }
    }
    
    ```

### @PostConstru 注解 && @PreDestroy 注解

    ```java
    package com.spring10;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.beans.factory.annotation.Qualifier;
    
    /**
     * Created by zeopean on 16/8/23.
     */
    public class Profile {
        @Autowired
        @Qualifier("student1")
        private Student student;
    
        public Profile() {
            System.out.println("依赖文件使用中@!");
        }
    
        public void printAge()
        {
            System.out.println("Student Age: " + student.getAge());
        }
    
        public void printName()
        {
            System.out.println("Student Name: " + student.getName());
        }
    }
    
    ```

### @Configuration && @Bean

    ```java
    package com.spring12;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;
    
    /**
     * Created by zeopean on 16/8/24.
     */
    @Configuration
    public class HelloWorldConfig {
        @Bean
        public HelloWorld helloWorld()
        {
            return new HelloWorld();
        }
    }

    
    ```
    
