# 输入输出空值
在fastjson中，缺省是不输出空值的。无论Map中的null和对象属性中的null，序列化的时候都会被忽略不输出，这样会减少产生文本的大小。但如果需要输出空值怎么做呢？

### 使用SerializerFeature.WriteMapNullValue
```java
Model obj = ...;
JSON.toJSONString(obj, SerializerFeature.WriteMapNullValue);
```

### 空值特别处理
SerializerFeature      | 描述
-----------------------|----------------------------------
WriteNullListAsEmpty   | 将Collection类型字段的字段空值输出为[]
WriteNullStringAsEmpty | 将字符串类型字段的空值输出为空字符串 ""
WriteNullNumberAsZero  | 将数值类型字段的空值输出为0
WriteNullBooleanAsFalse| 将Boolean类型字段的空值输出为false

```java
class Model {
      public List<Objec> items;
}

Model obj = ....;

String text = JSON.toJSONString(obj, SerializerFeature.WriteMapNullValue, SerializerFeature.WriteNullListAsEmpty);
```
