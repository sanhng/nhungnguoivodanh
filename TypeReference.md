在fastjson中提供了一个用于处理泛型反序列化的类TypeReference。

```java
import com.alibaba.fastjson.TypeReference;

List<VO> list = JSON.parseObject("...", new TypeReference<List<VO>>() {});
```

在这里例子中，通过TypeReference能够解决List<T>中T的类型问题。

在1.2.9 & 1.1.49.android版本中，TypeReference支持泛型参数，方便一些框架实现通用的反序列化类。用法如下：

### 单参数例子
```java
public class Response<T> {
     public T data;
}
public static <T> Response<T> parseToMap(String json, Class<T> type) {
     return JSON.parseObject(json, 
                            new TypeReference<Response<T>>(type) {});
}
```

### 双参数例子
```java
public static <K, V> Map<K, V> parseToMap(String json, 
                                            Class<K> keyType, 
                                            Class<V> valueType) {
     return JSON.parseObject(json, 
                            new TypeReference<Map<K, V>>(keyType, valueType) {
                            });
}

// 可以这样使用
String json = "{1:{name:\"ddd\"},2:{name:\"zzz\"}}";
Map<Integer, Model> map = parseToMap(json, Integer.class, Model.class);
assertEquals("ddd", map.get(1).name);
assertEquals("zzz", map.get(2).name);
```
