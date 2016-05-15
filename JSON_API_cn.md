JSON这个类是fastjson API的入口，主要的功能都通过这个类提供。

### 序列化API
```java
package com.alibaba.fastjson;

public abstract class JSON {
    // 将Java对象序列化为JSON字符串，支持各种各种Java基本类型和JavaBean
    public static String toJSONString(Object object, SerializerFeature... features);

    // 将Java对象序列化为JSON字符串，返回JSON字符串的utf-8 bytes
    public static byte[] toJSONBytes(Object object, SerializerFeature... features);

    // 将Java对象序列化为JSON字符串，写入到Writer中
    public static void writeJSONString(Writer writer, 
                                       Object object, 
                                       SerializerFeature... features);

    // 将Java对象序列化为JSON字符串，按UTF-8编码写入到OutputStream中
    public static final int writeJSONString(OutputStream os, // 
                                            Object object, // 
                                            SerializerFeature... features);



}
```

### JSON字符串反序列化API
```java
package com.alibaba.fastjson;

public abstract class JSON {
    // 将JSON字符串反序列化为JavaBean
    public static <T> T parseObject(String jsonStr, 
                                    Class<T> clazz, 
                                    Feature... features);

    // 将JSON字符串反序列化为JavaBean
    public static <T> T parseObject(byte[] jsonBytes,  // UTF-8格式的JSON字符串
                                    Class<T> clazz, 
                                    Feature... features);

    // 将JSON字符串反序列化为泛型类型的JavaBean
    public static <T> T parseObject(String text, 
                                    TypeReference<T> type, 
                                    Feature... features);

    // 将JSON字符串反序列为JSONObject
    public static JSONObject parseObject(String text);
}
```

# Demo
### parse Tree
```java
import com.alibaba.fastjson.*;

JSONObject jsonObj = JSON.parseObject(jsonStr);
```

### parse POJO
```java
import com.alibaba.fastjson.JSON;

Model model = JSON.parseObject(jsonStr, Model.class);
```

### parse POJO Generic
```java
import com.alibaba.fastjson.JSON;

Type type = new TypeReference<List<Model>>() {}.getType(); 
List<Model> list = JSON.parseObject(jsonStr, type);
```

### convert POJO to json string
```java
import com.alibaba.fastjson.JSON;

Model model = ...; 
String jsonStr = JSON.toJSONString(model);
```

### convert POJO to json bytes
```java
import com.alibaba.fastjson.JSON;

Model model = ...; 
byte[] jsonBytes = JSON.toJSONBytes(model);
```

### write POJO as json string to OutputStream
```java
import com.alibaba.fastjson.JSON;

Model model = ...; 
OutputStream os;
JSON.writeJSONString(os, model);
```

### write POJO as json string to Writer
```java
import com.alibaba.fastjson.JSON;

Model model = ...; 
Writer writer = ...;
JSON.writeJSONString(writer, model);
```