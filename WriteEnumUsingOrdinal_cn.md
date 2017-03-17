# 如何序列化Enum时输出ordinal而不是name
在fastjson中，缺省的序列化设置JSON.DEFAULT_GENERATE_FEATURE配置了SerializerFeature.WriteEnumUsingName，所以输出是默认是name，如果不想使用name，有两种办法。

### 1. 序列化是使用一个serialzerFeatures，而不使用全局的serializerFeature配置。
```java
public static class Model {
    public Type type;
}

public static enum Type {
    Big, Medium, Small
}

public void test_enum_ordinal() throws Exception {
    Model model = new Model();
    model.type = Type.Big;

    int serializerFeatures = JSON.DEFAULT_GENERATE_FEATURE & ~SerializerFeature.WriteEnumUsingName.mask;
    String text = JSON.toJSONString(model, serializerFeatures);
    System.out.println(text);
}
```

### 2. 修改全局配置
```java
JSON.DEFAULT_GENERATE_FEATURE &= ~SerializerFeature.WriteEnumUsingName.mask;
```
