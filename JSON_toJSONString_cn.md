将java对象序列化为JSON字符串，fastjson提供了一个最简单的入口
```java
package com.alibaba.fastjson;

public abstract class JSON {
    public static String toJSONString(Object object);
}
```