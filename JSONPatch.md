在fastjson 1.2.71版本后，支持JSONPatch ( http://jsonpatch.com/ ).

# API
```java
package com.alibaba.fastjson;

public class JSONPatch {
     public static String apply(String original, String patch);
     public static Object apply(Object object, String patch);
}
```

# DEMO
```java
String original = "{\n" +
        "  \"baz\": \"qux\",\n" +
        "  \"foo\": \"bar\"\n" +
        "}";

String patch = "[\n" +
        "  { \"op\": \"replace\", \"path\": \"/baz\", \"value\": \"boo\" },\n" +
        "  { \"op\": \"add\", \"path\": \"/hello\", \"value\": [\"world\"] },\n" +
        "  { \"op\": \"remove\", \"path\": \"/foo\" }\n" +
        "]";

String result = JSONPatch.apply(original, patch);
assertEquals("{\"baz\":\"boo\",\"hello\":[\"world\"]}", result);
```