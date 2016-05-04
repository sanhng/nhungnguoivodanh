fastjson支持注册ObjectDeserializer实现自定义反序列化。要自定义序列化，首先需要实现一个ObjectDeserializer，然后注册到ParserConfig中。

# 相关API
### ObjectDeserializer 定义
```java
package com.alibaba.fastjson.parser.deserializer;

public interface ObjectDeserializer {
    <T> T deserialze(DefaultJSONParser parser, Type type, Object fieldName);
    
    int getFastMatchToken();
}
```

### 注册自定义ObjectDeserializer API
```
package com.alibaba.fastjson.parser;

public class ParserConfig {
    public void putDeserializer(Type type, ObjectDeserializer deserializer);
}
```

# Sample
### Model定义
```java
public static enum OrderActionEnum {
                                    FAIL(1), SUCC(0);

    private int code;

    OrderActionEnum(int code){
        this.code = code;
    }
}

public static class Msg {

    public OrderActionEnum actionEnum;
    public String          body;
}
```

### 自定义实现ObjectDeserializer
```java
public static class OrderActionEnumDeser implements ObjectDeserializer {

    @SuppressWarnings("unchecked")
    @Override
    public <T> T deserialze(DefaultJSONParser parser, Type type, Object fieldName) {
        Integer intValue = parser.parseObject(int.class);
        if (intValue == 1) {
            return (T) OrderActionEnum.FAIL;
        } else if (intValue == 0) {
            return (T) OrderActionEnum.SUCC;
        }
        throw new IllegalStateException();
    }

    @Override
    public int getFastMatchToken() {
        return JSONToken.LITERAL_INT;
    }

}
```

### 注册并使用ObjectDeserializer
```java
ParserConfig.getGlobalInstance().putDeserializer(OrderActionEnum.class, new OrderActionEnumDeser());

{
    Msg msg = JSON.parseObject("{\"actionEnum\":1,\"body\":\"A\"}", Msg.class);
    Assert.assertEquals(msg.body, "A");
    Assert.assertEquals(msg.actionEnum, OrderActionEnum.FAIL);
}
{
    Msg msg = JSON.parseObject("{\"actionEnum\":0,\"body\":\"B\"}", Msg.class);
    Assert.assertEquals(msg.body, "B");
    Assert.assertEquals(msg.actionEnum, OrderActionEnum.SUCC);
}
```