在android下，很多JavaBean被序列化的次数不多，首次序列化和反序列化时需要构造类型相关信息，性能开销很大。常规实现中，fastjson/gson在首次序列化和反序列化是大约是非首次30倍耗时，在fastjson-1.1.49.android中，首次初始化类型相关信息，一个类大约0.5ms，在gson中更慢，一个类大约2ms。针对这种情况，fastjson-1.1.49.android版本中提供了提升首次序列化/反序列化性能的API。

```java
public class SerializeConfig {
   public ObjectSerializer registerIfNotExists(Class<?> clazz, // 类型
                                                int classModifers, // 如果类型为public，使用Modifier.PUBLIC
                                                boolean fieldOnly, // 是否只有field，没有getter/setter
                                                boolean jsonTypeSupport, // 是否有@JSONType配置
                                                boolean jsonFieldSupport, // 是否有@JSONField配置
                                                boolean fieldGenericSupport // 是否有泛型信息
                                                );
}

public class ParserConfig {
    public ObjectDeserializer registerIfNotExists(Class<?> clazz, // 类
                                                  int classModifiers, // 如果类型为public，使用Modifier.PUBLIC
                                                  boolean fieldOnly, // 是否只有field，没有getter/setter
                                                  boolean jsonTypeSupport, // 是否有@JSONType配置
                                                  boolean jsonFieldSupport, // 是否有@JSONField配置
                                                  boolean fieldGenericSupport // 是否有泛型信息
                                                );
}
```
提供这样的API，根据类型所需要的情况，避免调用Class.getModifiers/getAnnotation/getGenericType/getMethods等开销较大的调用。

例如：
```java
ParserConfig.getGlobalInstance().registerIfNotExists(MediaContent.class, Modifier.PUBLIC, true, false, false, false);

SerializeConfig.getGlobalInstance().registerIfNotExists(MediaContent.class, Modifier.PUBLIC, true, false, false, false);
```
