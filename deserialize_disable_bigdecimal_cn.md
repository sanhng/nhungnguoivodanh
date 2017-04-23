fastjson缺省反序列化带小数点的数值类型为BigDecimal，因为在真实的业务中，float/double表示的二进制精度和直观理解的十进制精度不太一样。但还是存在使用float/double而不是BigDecimal的场景。

# 1. 全局关闭
```java
JSON.DEFAULT_PARSER_FEATURE &= ~Feature.UseBigDecimal.getMask();
```

# 2. 局部关闭
```
int disableDecimalFeature = JSON.DEFAULT_PARSER_FEATURE &= ~Feature.UseBigDecimal.getMask();

String json = "....";
Class type = JSONObject.class;
JSON.parseObject(json, type, disableDecimalFeature);
```