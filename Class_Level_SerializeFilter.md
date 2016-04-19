对于框架来说，如果在toJSONString的时候，传入SerializeFilter，会导致对所有的类型做过滤，性能会受到一定影响。在1.2.10版本之后，fastjson提供类级别的SerializeFilter支持。

```java
package com.alibaba.fastjson.serializer;

public class SerializeConfig {
	public void addFilter(Class<?> clazz, SerializeFilter filter);
}
```

## Sample
```java
public class ClassNameFilterTest extends TestCase {
    public void test_filter() throws Exception {
        NameFilter upcaseNameFilter = new NameFilter() {
            public String process(Object object, String name, Object value) {
                return name.toUpperCase();
            }
        };
        SerializeConfig.getGlobalInstance() //
                       .addFilter(A.class, upcaseNameFilter);
        
        Assert.assertEquals("{\"ID\":0}", JSON.toJSONString(new A()));
        Assert.assertEquals("{\"id\":0}", JSON.toJSONString(new B()));
    }

    public static class A {
        public int id;
    }

    public static class B {
        public int id;
    }
}
```