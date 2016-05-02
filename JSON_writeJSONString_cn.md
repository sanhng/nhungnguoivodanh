在1.2.11版本中，JSON类新增对OutputStream/Writer直接支持。
```java
package com.alibaba.fastjson;

public abstract class JSON {
   public static final int writeJSONString(OutputStream os, // 
                                             Object object, // 
                                             SerializerFeature... features) throws IOException;

    public static final int writeJSONString(OutputStream os, //
                                             Charset charset, //  
                                             Object object, // 
                                             SerializerFeature... features) throws IOException;

   public static final int writeJSONString(Writer os, // 
                                             Object object, // 
                                             SerializerFeature... features) throws IOException;
}
```

### Sample
```java
import com.alibaba.fastjson;
import java.nio.charset.Charset;
class Model {
    public int value;
}

Model model = new Model();
model.value = 1001;

OutputStream os = ...;
JSON.writeJSONString(os, model);
JSON.writeJSONString(os, Charset.from("GB18030"), model);

Writer writer = ...;
JSON.writeJSONString(os, model);
```