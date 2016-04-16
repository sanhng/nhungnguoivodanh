在fastjson中提供了一个用于处理泛型反序列化的类TypeReference。

```java
import com.alibaba.fastjson.TypeReference;

List<VO> list = JSON.parseObject("...", new TypeReference<List<VO>>() {});
```

在这里例子中，通过TypeReference能够解决List<T>中T的类型问题。

在1.2.9 & 1.1.49.android版本中，TypeReference支持泛型参数，用法如下：

```java
public static <K, V> Map<K, V> getJsonToMap(String json, Class<K> keyType, Class<V> valueType) {
    return JSON.parseObject(json, new TypeReference<Map<K, V>>(keyType, valueType) {});
}

public void test_for_issue_2() throws Exception {
    String json = "{1:{name:\"ddd\"},2:{name:\"zzz\"}}";
    Map<Integer, Model> map = getJsonToMap(json, Integer.class, Model.class);
    Assert.assertEquals("ddd", map.get(1).name);
    Assert.assertEquals("zzz", map.get(2).name);
}
```