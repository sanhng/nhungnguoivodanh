1.2.51之后，fastjon提供了根据JSONPath快速解析JSON的API，避免原来需要先解析完再做JSONPath处理，能显著提升性能。
```
final String json = "[\n" +
            "   {\n" +
            "      \"name\" : \"john\",\n" +
            "      \"gender\" : \"male\"\n" +
            "   },\n" +
            "   {\n" +
            "      \"name\" : \"ben\"\n" +
            "   }\n" +
            "]";

String result = JSONPath.extract(json, "$[0]['name','gender']").toString();
assertEquals("[\"john\",\"male\"]", result);
```