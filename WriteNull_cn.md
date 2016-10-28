# 输入输出空值
在fastjson中，缺省是不输出空值的。无论Map中的null和对象属性中的null，序列化的时候都会被忽略不输出，这样会减少产生文本的大小。但如果需要输出空值怎么做呢？

### 使用SerializerFeature.WriteMapNullValue
```java
Model obj = ...;
JSON.toJSONString(obj, SerializerFeature.WriteMapNullValue);
```