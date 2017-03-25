# 非静态内嵌类支持

### 静态内嵌类
```java
public class Model {
    public static class Item {
    }
}
```

### 非静态内嵌类
```java
public class Model {
    public class Item {
    }
}
```

非静态内嵌类，编译之后，构造函数的参数是外层的类。在上面的例子中，Item的构造函数是：
```java
Item (Model modelThis) {}
```
这样是的在反序列化时，构造内嵌类实例产生了一些麻烦，必须传入Model的实例。

## fastjson支持哪些场景的非静态内嵌类的反序列化？
### 1. 直接内嵌
```java
public class Model {
    public Item item;
    public class Item {
    }
}

Model model = JSON.parseObject("{\"item\":{}}", Model.class);
```

### 2. 直接List内嵌
```java
public class Model {
    public List<Item> items;
    public class Item {
    }
}

Model model = JSON.parseObject("{\"items\":[{}]}", Model.class);
```

### 3. 直接Map内嵌
```java
public class Model {
    public Map<String, Item> items;
    public class Item {
    }
}

Model model = JSON.parseObject("{\"items\":{\"123\":{}}}", Model.class);
```