GeoJSON是一种对各种地理数据结构进行编码的格式，基于JSON表示法的地理空间信息数据交换格式。具体规范参考官方网站 https://geojson.org/

# 类结构
```java
com.alibaba.fastjson.support.geo.Geometry
com.alibaba.fastjson.support.geo.GeometryCollection
com.alibaba.fastjson.support.geo.Feature
com.alibaba.fastjson.support.geo.FeatureCollection
com.alibaba.fastjson.support.geo.LineString
com.alibaba.fastjson.support.geo.MultiLineString
com.alibaba.fastjson.support.geo.Point
com.alibaba.fastjson.support.geo.MultiPoint
com.alibaba.fastjson.support.geo.Polygon
com.alibaba.fastjson.support.geo.MultiPolygon
```

# 使用举例
```java
String str = "{\n" +
        "    \"type\": \"MultiPoint\",\n" +
        "    \"coordinates\": [\n" +
        "        [100.0, 0.0],\n" +
        "        [101.0, 1.0]\n" +
        "    ]\n" +
        "}";

Geometry geometry = JSON.parseObject(str, Geometry.class);
assertEquals(MultiPoint.class, geometry.getClass());

assertEquals("{\"type\":\"MultiPoint\",\"coordinates\":[[100.0,0.0],[101.0,1.0]]}", JSON.toJSONString(geometry));

String str2 = JSON.toJSONString(geometry);
assertEquals(str2, JSON.toJSONString(JSON.parseObject(str2, Geometry.class)));
```