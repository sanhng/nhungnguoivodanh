```java
Map map = Collections.singletonMap("value", 123);

String json = JSON.toJSONString(map
        , SerializeConfig.globalInstance
        , new SerializeFilter[0]
        , null
        , JSON.DEFAULT_GENERATE_FEATURE & ~SerializerFeature.QuoteFieldNames.mask
);
assertEquals("{value:123}", json);
```