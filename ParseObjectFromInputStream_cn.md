在1.2.11版本中，fastjson新增加了对InputStream的支持支持。
```java
package com.alibaba.fastjson;

public abstract class JSON {
    public static <T> T parseObject(InputStream is, //
                                    Type type, //
                                    Feature... features) throws IOException;

    public static <T> T parseObject(InputStream is, //
                                    Charset charset, //
                                    Type type, //
                                    Feature... features) throws IOException;
}
```

### Sample
```java
import com.alibaba.fastjson;
import java.nio.charset.Charset;
class Model {
    public int value;
}

InputStream is = ...
Model model = JSON.parseObject(is, Model.class);
Model model2 = JSON.parseObject(is, Charset.from("UTF-8"), Model.class);
```