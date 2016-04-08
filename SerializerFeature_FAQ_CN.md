# WriteNonStringValueAsString
引入版本 1.2.9，用于将非字符串类型的boolean/char/byte/int/long/float/double/Boolean/Character/Byte/Integer/Long/Float/Double/BigInteger/BigDecimal输出为字符串类型。

```java
public class VO {
    public boolean id;
}

VO vo = new VO();
vo.id = true;

Assert.assertEquals("{\"id\":\"true\"}"
        , JSON.toJSONString(vo, SerializerFeature.WriteNonStringValueAsString));
Assert.assertEquals("{\"id\":true}", JSON.toJSONString(vo));
```