1.2.60新增加一个高性能校验JSON字符串的API，还在验证阶段，欢迎试用。支持输入类型是字符串、byte数组、InputStream、Reader。

# 1. JSONValidator API

```java
package com.alibaba.fastjson;

public abstract class JSONValidator {
    // 支持输入类型是utf8编码的byte[]、String、InputStream、Reader
    public static JSONValidator fromUtf8(byte[] jsonBytes)
    public static JSONValidator fromUtf8(InputStream is)
    public static JSONValidator from(String str)
    public static JSONValidator from(Reader r)

    public boolean validate();
}
```

# 2. JSON字符串校验
``` java
String jsonStr = ...
JSONValidator validator = JSONValidator.from(jsonStr);
boolean valid = validator.validate();
```


# 3. UTF8 byte数组校验
输入参数是byte[]时，只支持UTF8编码
``` java
byte[] jsonBytes = ...
JSONValidator validator = JSONValidator.fromUtf8(jsonBytes);
boolean valid = validator.validate();
```

# 4. InputStream校验
输入参数是InputSteam时，只支持UTF8编码
``` java
InputStream is = ...
JSONValidator validator = JSONValidator.fromUtf8(is);
boolean valid = validator.validate();
```

# 5. Reader校验
``` java
Reader r = ...
JSONValidator validator = JSONValidator.from(r);
boolean valid = validator.validate();
```