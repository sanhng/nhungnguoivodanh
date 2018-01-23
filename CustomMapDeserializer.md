在某些场景下，需要对JSON中的Key忽略大小写处理。fastjson 1.2.44版本提供了支持。
```java
import com.alibaba.fastjson.JSON;
import com.alibaba.fastjson.parser.Feature;
import com.alibaba.fastjson.parser.ParserConfig;
import com.alibaba.fastjson.parser.deserializer.MapDeserializer;
import junit.framework.TestCase;
import org.apache.commons.collections4.map.*;

ParserConfig config = new ParserConfig();
MapDeserializer deserializer = new MapDeserializer() {
    public Map<Object, Object> createMap(Type type) {
        return new CaseInsensitiveMap();
    }
};
config.putDeserializer(Map.class, deserializer);

CaseInsensitiveMap<String, Object> root = (CaseInsensitiveMap) JSON.parseObject("{\"val\":{}}", Map.class, config, Feature.CustomMapDeserializer);
CaseInsensitiveMap subMap = (CaseInsensitiveMap) root.get("val");
assertEquals(0, subMap.size());
```