在1.2.31版本中，fastjson引入了JSONField.unwrapped配置，使得定制序列化和反序列化更加方便。

# Demo 1
```java
public static class VO {
    public int id;

    @JSONField(unwrapped = true)
    public Localtion localtion;
}

public static class Localtion {
    public int longitude;
    public int latitude;

    public Localtion() {}

    public Localtion(int longitude, int latitude) {
        this.longitude = longitude;
        this.latitude = latitude;
    }
}

VO vo = new VO();
vo.id = 123;
vo.localtion = new Localtion(127, 37);

String text = JSON.toJSONString(vo);
Assert.assertEquals("{\"id\":123,\"latitude\":37,\"longitude\":127}", text);

VO vo2 = JSON.parseObject(text, VO.class);
assertNotNull(vo2.localtion);
assertEquals(vo.localtion.latitude, vo2.localtion.latitude);
assertEquals(vo.localtion.longitude, vo2.localtion.longitude);
```