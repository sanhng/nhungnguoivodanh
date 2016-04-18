在某些场景下，对Value做过滤，需要获得所属JavaBean的信息，包括类型、字段、方法等。在fastjson-1.2.9中，提供了ContextValueFilter，类似于之前版本提供的ValueFilter，只是多了SeriliazeContext参数可用。

```java
package com.alibaba.fastjson.serializer;

public interface ContextValueFilter extends SerializeFilter {
    Object process(SerializeContext context, 
                   Object object, 
                   String name, 
                   Object value);
}
```

其中SerializeContext的定义如下：
```java
package com.alibaba.fastjson.serializer;

public final class SerializeContext {
    public Class<?> getBeanClass();

    public Method getMethod();

    public Field getField();

    public String getName();

    public String getLabel();
}
```

### 例子
```java
ContextValueFilter valueFilter = new ContextValueFilter() {
    public Object process(SerializeContext context, 
                          Object object, 
                          String name, 
                          Object value) {
        Class<?> objectClass = context.getBeanClass();
        UrlIdentify annotation = context.getAnnation(UrlIdentify.class);
        
        // ....
        
        return value;
    }
};

JSON.toJSONString(model, valueFilter);
```