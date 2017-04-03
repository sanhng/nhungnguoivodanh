在1.2.31版本中，引入了一个特性，序列化是支持unwrapped配置。

## 用法
通过JSONField配置在field或者getter方法上。
```java
@JSONField(unwrapped = true)
```

## demo
```java
public static class VO {
    public int id;
    
    @JSONField(unwrapped = true)
    public Localtion localtion;
}

public static class Localtion {
    public int longitude;
    public int latitude;

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
``