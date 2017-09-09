###  Set  


#### HashSet

1.添加元素
```

HashSet hashSet = new HashSet();
hashSet.add("Java");
        
```

2.删除元素

```
HashSet hashSet = new HashSet();
hashSet.add("Java");
hashSet.remove("Java"):

```

####  TreeSet

```
         TreeSet nums = new TreeSet();

        //添加元素
        nums.add(5);
        nums.add(52);
        nums.add(-5);
        nums.add(520);

        System.out.println(nums);

        System.out.println("------------------");

		 //第一个元素
        Integer first = (Integer) nums.first();
		 //最后一个元素
        Integer last = (Integer) nums.last();
		 //小于5的集合
        TreeSet headSet = (TreeSet) nums.headSet(5);
		 //大于5的集合
        TreeSet tailSet = (TreeSet) nums.tailSet(5);
		 //大于－6，小于6 的集合
        TreeSet subSet = (TreeSet) nums.subSet(-6, 6);
``` 

#### EnumSet


```
		public enum Season {
		    SPRING, SUMMER, FALL, WINTER
		}


        //创建EnumSet集合
        EnumSet enumSet = EnumSet.allOf(Season.class);
        System.out.println(enumSet);

        //创建空集合
        EnumSet enumSet1 = EnumSet.noneOf(Season.class);
        System.out.println(enumSet1);

        //添加元素
        enumSet1.add(Season.WINTER);
        enumSet1.add(Season.SPRING);

        System.out.println(enumSet1);

        //指定值创建集合
        EnumSet enumSet2 = EnumSet.of(Season.SPRING, Season.FALL);
        System.out.println(enumSet2);

        //差集
        EnumSet enumSet3 = EnumSet.complementOf(enumSet2);
        System.out.println(enumSet3);


```

### List  

#### ArrayList

```
public static void main(String[] args) {

        List books = new ArrayList<>();
        //添加元素
        books.add(new String("php"));
        books.add(new String("Java"));
        books.add(new Integer(1));
        books.add(true);
        System.out.println(books);

        //在下标为1处 插入新的对象
        books.add(1, new String("Python"));
        System.out.println(books);

        //删除下标为 2 的元素
        books.remove(2);
        System.out.println(books);

        //元素定位
        Integer index = books.indexOf(new String("php"));
        //元素截取
        List subList = books.subList(0, 2);
}


```

#### Stack

```

        LinkedList books = new LinkedList();

        books.add(1);

        //尾部添加元素
        books.offer("python");
        //栈顶部添加元素
        books.push("java");

        books.add(2);

        //访问栈顶元素
        System.out.println(books.peekFirst());

        //访问栈尾元素
        System.out.println(books.peekLast());

        //出栈
        System.out.println(books.pop());

        //删除顶部元素
        System.out.println(books.poll());
        

```


### Queue

#### PriorityQueue

```

        PriorityQueue priorityQueue = new PriorityQueue();

        //向队列中添加元素
        priorityQueue.offer(8);
        priorityQueue.offer(9);
        priorityQueue.offer(0);
        priorityQueue.offer(-1);

		  // 元素值不能是null
//        priorityQueue.offer(null);

        // 删除元素
        priorityQueue.poll();

```

#### iterator 迭代器

```

		 //创建集合对象
        Collection collection = new HashSet<>();
        collection.add("java");
        collection.add("python");
        collection.add("c++");
        collection.add("php");

        //迭代器
        Iterator iterator = collection.iterator();

        while (iterator.hasNext()) {
            String col = (String) iterator.next();
            System.out.println(col);

            if (col.equals("c++")) {
                iterator.remove();
            }
        }

        System.out.println(collection);
        

```

#### foreach 遍历

```

        //创建集合对象
        Collection collection = new HashSet<>();
        collection.add("java");
        collection.add("python");
        collection.add("c++");
        collection.add("php");

        for (Object object : collection) {
            String col = (String) object;
            System.out.println(col);
        }
        

```

### Map

#### hashTable 

```

        Hashtable hashtable = new Hashtable();
        hashtable.put(new MapA(100), "java");
        hashtable.put(new MapA(200), "python");
        hashtable.put(new MapA(300), "php");
        hashtable.put(new MapA(400), "c");

        Object obj = hashtable.containsValue("python8"); //比较集合值

        Object keys = hashtable.containsKey(100); //比较集合键
		 //删除元素
        hashtable.remove(new MapA(100));

        //foreach 遍历
        for (Object key : hashtable.keySet()) {
            System.out.println(key);
            System.out.println(hashtable.get(key));
        }

```

#### LinkedHashMap

```

        LinkedHashMap scores = new LinkedHashMap();

        //添加元素
        scores.put("english", 80);
        scores.put("yuwen", 180);
        scores.put("shuxue", 800);

        //遍历元素
        for (Object key : scores.keySet()) {
            System.out.println(key + "----" + scores.get(key));
        }

```


#### Properties

```

        Properties properties = new Properties();
        //向 properties 添加元素
        properties.setProperty("username", "zeopean");
        properties.setProperty("age", "1");
        properties.setProperty("key", "false");

```


#### TreeMap 

```

        TreeMap treeMap = new TreeMap();
        treeMap.put(new TreeMapR(9), "java");
        treeMap.put(new TreeMapR(19), "python");
        treeMap.put(new TreeMapR(-9), "c++");

        //获取第一个元素
        Object object = treeMap.firstEntry();
        //获取最后一个元素
        Object object1 = treeMap.lastEntry();
        //获取第一个key
        Object object2 = treeMap.firstKey();
        //获取最后一个key
        Object object3 = treeMap.lastKey();

        //返回该TreeMap的比new TreeMapR(2)大的最小 key/key-value 值。
        Object object4 = treeMap.higherEntry(new TreeMapR(2));
        Object object5 = treeMap.higherKey(new TreeMapR(2));

        //返回该TreeMap的比new TreeMapR(2)小的最大的key-value对。
        Object object6 = treeMap.lowerKey(new TreeMapR(2));
        Object object7 = treeMap.lowerEntry(new TreeMapR(2));

        //获取 子集 map
        Object object8 = treeMap.subMap(new TreeMapR(-10), new TreeMapR(10));

```

