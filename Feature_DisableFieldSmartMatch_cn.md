如果输入json文本和JavaBean的属性不是精确匹配时，fastjson会通过多种匹配方式查找属性，会消耗较多的资源。在1.2.30中，引入了Feature.DisableFieldSmartMatch ，可以解决这个问题。

## 通过@JSONType配置
```java
@JSONType(parseFeatures = Feature.DisableFieldSmartMatch)
public static class Model_for_disableFieldSmartMatchMask2 {
    public int personId;
}

assertEquals(0, JSON.parseObject("{\"person_id\":123}", Model_for_disableFieldSmartMatchMask2.class).personId);
```

## 调用toJSONString时传入参数
```java
public static class Model_for_disableFieldSmartMatchMask {
    public int personId;
}

assertEquals(123
          , JSON.parseObject("{\"person_id\":123}"
                           , Model_for_disableFieldSmartMatchMask.class).personId);
assertEquals(0
           , JSON.parseObject("{\"person_id\":123}"
                            , Model_for_disableFieldSmartMatchMask.class, Feature.DisableFieldSmartMatch).personId);
```
