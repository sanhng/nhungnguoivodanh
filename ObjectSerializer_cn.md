fastjson提供了自定义序列化的接口，当你通过配置无法满足自定义序列化需求时，你可以使用ObjectSerializer接口。

# 相关API 
### ObjectSerializer接口
```java
package com.alibaba.fastjson.serializer;

public interface ObjectSerializer {
    void write(JSONSerializer serializer, 
               Object object, 
               Object fieldName, 
               Type fieldType, 
               int features) throws IOException;
}
```

### 注册API
```java
package com.alibaba.fastjson.serializer;

public class SerializeConfig {
	public boolean put(Type key, ObjectSerializer value);
}
```

# Sample
```java
public class CharacterCodec implements ObjectSerializer {
    public void write(JSONSerializer serializer, 
                      Object object, 
                      Object fieldName, 
                      Type fieldType, 
                      int features) throws IOException {
        SerializeWriter out = serializer.out;
    
        Character value = (Character) object;
        if (value == null) {
            out.writeString("");
            return;
        }
    
        char c = value.charValue();
        if (c == 0) {
            out.writeString("\u0000");
        } else {
            out.writeString(value.toString());
        }
    }
}
```