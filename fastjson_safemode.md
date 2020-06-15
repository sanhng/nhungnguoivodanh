## 打开SafeMode功能
在1.2.68之后的版本，在1.2.68版本中，fastjson增加了safeMode的支持。safeMode打开后，完全禁用autoType。所有的安全修复版本sec10也支持SafeMode配置。

有三种方式配置SafeMode，如下:<br/>
### 1. 在代码中配置
```java
ParserConfig.getGlobalInstance().setSafeMode(true); 
```
* 注意，如果使用new ParserConfig的方式，需要注意单例处理，否则会导致低性能full gc。


### 2. 加上JVM启动参数
```script
    -Dfastjson.parser.safeMode=true 
```
如果有多个包名前缀，用逗号隔开

### 3. 通过fastjson.properties文件配置。
通过类路径的fastjson.properties文件来配置，配置方式如下：
```
fastjson.parser.safeMode=true
```

### 4. safeMode场景如何做autoType
在1.2.68之后的版本，提供了AutoTypeCheckHandler扩展，可以自定义类接管autoType, 通过ParserConfig#addAutoTypeCheckHandler方法注册。

```
// com.alibaba.fastjson.parser.ParserConfig.AutoTypeCheckHandler
    /**
     * @since 1.2.68
     */
    public interface AutoTypeCheckHandler {
        Class<?> handler(String typeName, Class<?> expectClass, int features);
    }

    // com.alibaba.fastjson.parser.ParserConfig#addAutoTypeCheckHandler
```

### 5. 怎么判断是否用到了autoType
看序列化的代码中是否用到了SerializerFeature.WriteClassName
```java
JSON.toJSONString(obj, SerializerFeature.WriteClassName); // 这种使用会产生@type
```

### 6. 使用JSONType.autoTypeCheckHandler
在fastjson 1.2.71版本中，提供了通过JSONType配置autoTypeCheckHandler的方法，比如：
```java
public class JSONTypeAutoTypeCheckHandlerTest extends TestCase {
    public void test_for_checkAutoType() throws Exception {
        Cat cat = (Cat) JSON.parseObject("{\"@type\":\"Cat\",\"catId\":123}", Animal.class);
        assertEquals(123, cat.catId);
    }

    @JSONType(autoTypeCheckHandler = MyAutoTypeCheckHandler.class)
    public static class Animal {

    }

    public static class Cat extends Animal {
        public int catId;
    }

    public static class Mouse extends Animal {

    }

    public static class MyAutoTypeCheckHandler implements ParserConfig.AutoTypeCheckHandler {

        public Class<?> handler(String typeName, Class<?> expectClass, int features) {
            if ("Cat".equals(typeName)) {
                return Cat.class;
            }

            if ("Mouse".equals(typeName)) {
                return Mouse.class;
            }

            return null;
        }
    }
}
```

