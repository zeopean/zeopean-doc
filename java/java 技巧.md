#### java 线程锁定 synchronized

```
synchronized public static LazySingleton getInstance() {   
        if (instance == null) {  
            instance = new LazySingleton();   
        }  
        return instance;   
    }  


public static LazySingleton getInstance() {   
    if (instance == null) {  
        synchronized (LazySingleton.class) {  
            instance = new LazySingleton();   
        }  
    }  
    return instance;   
}
```

#### java 读取xml 创建类对象

```
 public static Object getBean(){
        try {
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
            DocumentBuilder builder = factory.newDocumentBuilder();
            File file = new File("/Users/zeopean/IdeaProjects/Pattern/config_builder.xml");
            System.out.println(file.isFile());
            Document doc ;
            doc = builder.parse(file.toString());

            //获取文本节点
            NodeList nodeList = doc.getElementsByTagName("className");
            Node node = nodeList.item(0).getFirstChild();
            String name = node.getNodeValue();

            Object obj = Class.forName("com.builder."+name).newInstance();
            return obj;

        } catch (Exception e){
            e.printStackTrace();
            return null;
        }
    }

```