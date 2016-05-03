JSON这个类是fastjson API的入口，主要的功能都通过这个类提供。

```java
package com.alibaba.fastjson;

public abstract class JSON {
    // 将Java对象序列化为JSON字符串，支持各种各种Java基本类型和JavaBean
    public static String toJSONString(Object object, SerializerFeature... features);

    // 将JSON字符串反序列化为JavaBean
    public static <T> T parseObject(String text, Class<T> clazz, Feature... features);

    // 将JSON字符串反序列化为泛型类型的JavaBean
    public static <T> T parseObject(String text, TypeReference<T> type, Feature... features);

    public static JSONObject parseObject(String text);

}
```