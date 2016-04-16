在fastjson-1.2.9版本后提供了ExtraProcessable接口，用于定制对象的反序列化功能。接口如下
```java
/**
 * @since 1.2.9
 */
public interface ExtraProcessable {
    void processExtra(String key, Object value);
}
```

如果对象没有对应public setter和public field，就会调用processExtra方法。这个可以用于一些框架实现MapBean对象的json序列化和反序列化。

例如
```java
import java.io.IOException;
import java.lang.reflect.Type;
import java.util.*;

import org.junit.Assert;
import junit.framework.TestCase;

import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.parser.deserializer.ExtraProcessable;
import com.alibaba.fastjson.serializer.*;

public class Bug_for_issue_265 extends TestCase {

    public void test_for_issue() throws Exception {
        User user = new User();
        user.setName("wenshao");
        
        String text = JSON.toJSONString(user);
        
        Assert.assertEquals("{\"name\":\"wenshao\"}", text);
        
    }
    
    public void test_for_issue_decode() throws Exception {
        String text = "{\"name\":\"wenshao\",\"id\":1001}";
        
        User user = JSON.parseObject(text, User.class);
        Assert.assertEquals("wenshao", user.getName());
        Assert.assertEquals(1001, user.getAttribute("id"));
    }

    public static class Model implements JSONSerializable, ExtraProcessable {

        protected Map<String, Object> attributes = new HashMap<String, Object>();

        public Map<String, Object> getAttributes() {
            return attributes;
        }
        
        public Object getAttribute(String name) {
            return attributes.get(name);
        }

        @Override
        public void write(JSONSerializer serializer, Object fieldName, Type fieldType,
                          int features) throws IOException {
            serializer.write(attributes);
        }

        @Override
        public void processExtra(String key, Object value) {
            attributes.put(key, value);
        }
    }

    public static class User extends Model {

        public String getName() {
            return (String) attributes.get("name");
        }

        public void setName(String name) {
            attributes.put("name", name);
        }
    }
}
```