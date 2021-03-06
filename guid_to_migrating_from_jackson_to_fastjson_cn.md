jackson也是一个很优秀的jackson库，但是如果你因为某些理由想迁移到fastjson，这个指南将会为你介绍如何从jackson迁移到fastjson。

# Annotions
在fastjson中，有四个Annotation，JSONType、JSONField、JSONCreator、JSONPOJOBuilder，能够完成jackson大多数Annotation对应的功能。

### 1. JsonView迁移
在fastjson中，提供有一个LabelFilter，能够实现Jackson JsonView的功能，用于定制序列化。详细文档
 https://github.com/alibaba/fastjson/wiki/LabelFilter

### 2. JsonPOJOBuilder
在Jackson中提供了对Builder模式支持的JsonPOJOBuilder，在fastjson中对应的是JSONPOJOBuilder。详细文档 https://github.com/alibaba/fastjson/wiki/BuilderSupport

### 3. JsonAnyGetter & JsonAnySetter & JsonUnwrapped
在fastjson 1.2.32版本中引入JSONField.unwrapped配置，支持类似JsonAnyGetter/JsonAnySetter的功能，详细文档 https://github.com/alibaba/fastjson/wiki/JSONField_unwrapped_cn

### 4. JsonPropertyOrder
在fastjson的JSONType.orders提供了同样的功能。例如：
```java
@JSONType(orders={"name", "id"})
public static class VO {
    public int    id;
    public String name;
}
```

### 5. JsonRawValue
在fastjson中，通过JSONField.jsonDirect配置能实现同样的功能。
```java
public static class Model {
    public int id;
    @JSONField(jsonDirect=true)
    public String value;
}
```

### 6. JsonSerialize
在fastjson中，可以通过使用JSONField.serializeUsing和JSONType.serializer实现同样的功能。

### 7. JsonCreator
在fastjson中有对应的JSONCreator

### 8. JsonSetter
在fastjson中，可以用JSONField实现同样的功能。

### 9. JsonDeserialize
在fastjson中，可以通过使用JSONField.deserializeUsing和JSONType.deserializer实现同样的功能。

### 10. JsonIgnoreProperties
在fastjson中，可以通过使用JSONType.ignores实现同样的功能

### 11. JsonIgnore
在fastjson中，可以通过使用JSONField.serilaize=false和JSONField.deserilaize=false和实现同样的功能

### 12. JsonFormat
在fastjson中，可以通过使用JSONField.format实现同样的功能

### 13. Jackson Polymorphic Type Handling Annotations
在fastjson中，可以通过JSONType.seeAlso实现类似的功能。详细文档 https://github.com/alibaba/fastjson/wiki/JSONType_seeAlso_cn