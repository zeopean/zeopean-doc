
### List

```java

    public static void listTest()
    {
        List<String> list = new ArrayList<>();  //创建list
        list.add("hello ");
        list.add("zeopean");

        Iterator<String> iterator = list.iterator();    //迭代器
        int i = 0;
        while(iterator.hasNext())       //数据遍历
        {
            String value = iterator.next();
            i++;
            System.out.println(value + " i " + i);
        }

        System.out.println(list);
    }
    
```

### ArrayList

```java
    public static void arrayListTest()      //List 的几种遍历方式时效的比较
    {
        List<String> list = new ArrayList<String>();
        long t1,t2;
        for(int j = 0; j < 40000; j++)
        {
            list.add("aaaaaa" + j);
        }
        System.out.println("List first visit method:");
        t1=System.currentTimeMillis();
        for(String tmp:list)
        {
            System.out.println(tmp);
        }
        t2=System.currentTimeMillis();
        System.out.println("Run Time:" + (t2 -t1) + "(ms)");
        System.out.println("List second visit method:");

        t1=System.currentTimeMillis();
        for(int i = 0; i < list.size(); i++)
        {
            list.get(i);
            //System.out.println(list.get(i));
        }
        t2=System.currentTimeMillis();
        System.out.println("Run Time:" + (t2 -t1) + "(ms)");

        System.out.println("List Third visit method:");
        Iterator<String> iter = list.iterator();

        t1=System.currentTimeMillis();
        while(iter.hasNext())
        {
            iter.next();
        }
        t2=System.currentTimeMillis();
        System.out.println("Run Time:" + (t2 -t1) + "(ms)");

        System.out.println(" Finished ! ");

    }

```

### Map

```java

    public static void mapTest()
    {
        HashMap<String , String> map = new HashMap<>();     //创建map

        map.put("1" ,"zeopean");        //插入数据
        map.put("2" , "daming");

        //遍历数据
        Iterator<String> iterator = map.keySet().iterator() ;   //创建迭代器
        while(iterator.hasNext())       //进行数据遍历
        {
            Object key = iterator.next();   //获取键名
            System.out.print("key = " + key);
            System.out.println(", value = " + map.get(key));    //获取键值
        }

        System.out.println("\n");


        Iterator entries = map.entrySet().iterator();
        while(entries.hasNext())
        {
            Map.Entry entry = (Map.Entry) entries.next();
            Object key = entry.getKey();
            Object value = entry.getValue();

            System.out.println("key = " + key + ", value = " + value);
        }
        System.out.println("is end ! ");

    }
```

### Set

```java

    public static void setTest()
    {
        Set<String> set1 = new HashSet<String>();   //  创建set
        set1.add("s1_1");       //添加数据
        set1.add("s1_2");
        set1.add("s1_3");
        set1.add("one");

        System.out.println(set1);

        Set<String> set2 = new HashSet<>();
        set2.add("set_1");
        set2.add("set_2");
        set2.add("set_3");

        System.out.println(set2);
    }
    
```

