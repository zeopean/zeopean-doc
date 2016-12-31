
### byName 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- bean 的自动加载 byName -->
    <bean id="textEditor" class="com.spring05.TextEditor" autowire="byName">
        <property name="name" value="zeopean test"/>
    </bean>

    <bean id="SpellChecker" class="com.spring05.SpellChecker">

    </bean>

</beans>
```

### byType
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- bean 的自动加载 byType-->
    <bean id="textEditor" class="com.spring06.TextEditor" autowire="byType">
        <property name="name" value="zeopean test"/>
    </bean>

    <bean id="SpellChecker" class="com.spring06.SpellChecker">

    </bean>

</beans>
```


### contructor
```xml

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- bean 的自动加载 constructor-->
    <bean id="textEditor" class="com.spring06.TextEditor" autowire="constructor">
        <property name="name" value="zeopean test"/>
    </bean>

    <bean id="SpellChecker" class="com.spring06.SpellChecker">

    </bean>

</beans>

```