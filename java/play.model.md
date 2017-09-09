-- 设置表名
```
@Table(name = "tb_account")
@Entity
public class Account extends BaseModel implements java.io.Serializable 

```


-- 获取一条数据

```
-- 根据account_id 获取
employeeTest = employeeTest.find("byAccountId", accountId).first();

-- 根据username && password 获取
Account account = Account.find("byUsernameAndPassword", username, password).first();


```

-- 原生sql 查询

```
List<Question> qList = JPA.em().createQuery(
                "select q from Question q where q.id in (select questionId from ModuleQuestion where moduleId = ?)")//
                .setParameter(1, moduleId).getResultList();

```


-- 获取属性

```
employeeTest.getIsCompleted()

```

-- 为json对象添加属性

```

testStatejsonObject.addProperty("username", userNameArray[i]);


```