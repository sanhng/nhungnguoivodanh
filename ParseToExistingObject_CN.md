为了避免在parse成JSONObject之后，进行put操作导致内部的map扩容，可以先定义好JSONObject的容量。，然后使用DefaultJSONParser来进行解析。

```
JSONObject obj = new JSONObject(1024);

String text = "...";
DefaultJSONParser parser = new DefaultJSONParser(text);
parser.parseObject(obj); // parse to existing object
```