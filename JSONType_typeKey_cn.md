在某些场景，需要使用非缺省typeKey，在1.1.58.android支持@JSONType.typeKey配置。

```java
@JSONType(seeAlso = {FloorV2.class}, typeKey = "type")
public interface Area {
    public static final String TYPE_SECTION = "section";
    public static final String TYPE_FLOORV1 = "floorV1";
    public static final String TYPE_FLOORV2 = "floorV2";
}

@JSONType(typeName = "floorV2")
public static class FloorV2 implements Area {
    public String type;

    public String templateId;
}

// testcase code
String json = "{\"type\":\"floorV2\",\"templateId\":\"x123\"}";

FloorV2 floorV2 = (FloorV2) JSON.parseObject(json, Area.class);
assertNotNull(floorV2);
assertNotNull(floorV2.templateId);
assertEquals("x123", floorV2.templateId);
assertEquals("floorV2", floorV2.type);

String json2 = JSON.toJSONString(floorV2, SerializerFeature.WriteClassName);
assertEquals("{\"type\":\"floorV2\",\"templateId\":\"x123\"}", json2);
```
