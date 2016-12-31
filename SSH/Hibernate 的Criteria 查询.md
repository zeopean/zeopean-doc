
#### Criteria 的使用示例：

```java

Criteria criteria = session.createCriteria(User.class);

criteria.add(Restrictions.like("name", "just%"));

List users = criteria.list();

```

#### Restructions 的方法有：

Restrictions的幾個常用限定查詢方法如下表所示：


方 法|	說 明
---|---|
Restrictions.eq	|等於Restrictions.allEq	使用Map，使用key/value進行多個等於的比對
Restrictions.gt	|大於 >
Restrictions.ge	|大於等於 >=
Restrictions.lt	|小於 <
Restrictions.le	|小於等於 <=
Restrictions.between	|對應SQL的BETWEEN子句
Restrictions.like	|對應SQL的LIKE子句
Restrictions.in	    |對應SQL的in子句
Restrictions.and	|and關係
Restrictions.or	    |or關係
Restrictions.sqlRestriction	|SQL限定查詢


#### Criteria 排序

```
    public static void main(String[] args) {
        Session session = HibernateUtil.getSessionFactory().openSession();

        //stati
        Criteria criteria3 = session.createCriteria(UserEntity.class);
        criteria3.setProjection(Projections.avg("age"));
        List users3 = criteria3.list();

        System.out.print(users3);
    }
    ```
        
        

#### Criteria 分组
```
    public static void main(String[] args) {
        Session session = HibernateUtil.getSessionFactory().openSession();

        //group by
        Criteria criteria2 = session.createCriteria(UserEntity.class);
        criteria2.setProjection(Projections.groupProperty("age"));
        List user2 = criteria2.list();

        System.out.print(user2);

    }
```


