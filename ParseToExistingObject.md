
# Parse to an existing object

```java
JSONObject obj = new JSONObject(1024);

String text = "...";
DefaultJSONParser parser = new DefaultJSONParser(text);
parser.parseObject(obj); // parse to existing object
```