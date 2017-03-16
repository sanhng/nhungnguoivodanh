# 已知影响兼容的变更
1. JSONLexer在1.1.32~1.1.34版本中是class，其他版本是interface
2. JSON#handleResovleTask方法不兼容问题，在
	1.1.15返回值是void
	1.1.16~1.1.33版本之前返回类型是int，
	1.1.34~1.1.41版本返回void
	1.1.42~1.1.46方法移到JSONParser中
3. com.alibaba.fastjson.util.Base64/com.alibaba.fastjson.util.ThreadLocalCache类在1.2.9版本被删除
4. 1.2.x中，ObjectSerializer.write方法和ObjectDeserializer
5. ObjectSerializer/ObjectDeserializer定制序列化，从1.1.x升级到1.2.x会有兼容问题。
6. 打开SerializerFeature.UseISO8601DateFormat时，序列化java.util.Date类型，在1.1.15~1.2.4不带时区，1.2.5及之后版本带时区。
7. 1.2.9~1.2.13版本JSONObject去掉了serialVersionUID字段，会导致Java反序列化不兼容问题
8. 1.2.3之后的版本，Map的序列化没有做排序再输出，原因是通过TreeMap排序很影响性能。1.2.27版本中增加SerializerFeature.MapSortField实现同样的功能。
	使用方法如下：
	a) 传入SerializerFeature.MapSortField参数。
		JSON.toJSONString(map, SerializerFeature.MapSortField);
	b) 通过代码修改全局缺省配置。
		JSON.DEFAULT_GENERATE_FEATURE |= SerializerFeature.MapSortField.getMask();
	c) 通过JVM启动参数配置修改全局配置
		-Dfastjson.serializerFeatures.MapSortField=true
	d) 通过类路径下的fastjson.properties来配置
		fastjson.serializerFeatures.MapSortField=true

9. com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter在1.2.10后会在Header中设置ContentLength
10. 1.1.33及之后版本中删除com.alibaba.fastjson.util.AntiCollisionHashMap，会导致Java反序列化不兼容 （1.2.26版本中已经补上）
11. 1.2.10之后的版本，com.alibaba.fastjson.TypeReference去掉了LIST_STRING属性 （1.2.26版本中已经补上）
12. 1.1.21~1.2.25版本中，如果List类型字段配置了JSONField时，parse时不能识别大小写不匹配的情况。 (1.2.26版本中修正)
13. 1.2.11~1.2.25版本中，com.alibaba.fastjson.util.IOUtils类删除了readAll方法。（1.2.26版本中已经补上）
14. 1.2.11~1.2.26版本中，如果输入byte[]，并且包含中文字符串的，会有JDK 1.6/1.5不兼容问题。 （1.2.27版本修复）
15. 1.2.9~1.2.26版本中，存在Enum字段类型并且使用了SerializerFilter，序列化时会NoSuchFieldError错误。 （1.2.27版本修复）
16. 1.2.9~1.2.26版本中，会自动识别下划线开头的key，比如：{"id":1001,"_id":1002} 这种场景，如果JavaBean中有id字段，最后会得到1002，之前的版本是1001。（在1.2.27版本中修复）
17. 1.2.9之后的版本，对日期格式有严格的校验，"0017-02-12 01:46:17.0"这种格式的日期会报错。
18. 1.2.13之后的版本，{"isSuccess":}这种字段，能够识别到boolean success字段中，如果isSuccess后的值不规范，会报错。比如{"isSucess":"Y"}在1.2.12及之前版本是之前版本是会被忽略，1.2.13及之后版本会报错。
19. 1.2.23~1.2.26版本中，如果实际存储和泛型参数不一致的情况，会报错。比如：
```java
public static class Base<T> {
    public T id;
}
public static class Model extends Base<Long> { }

Model model = new Model();
Base base = model;
base.id = BigInteger.valueOf(3); // 通过Base直接赋值非Long类型, 在1.2.23~1.2.26版本中toJSONString会报错
JSON.toJSONString(base);
```

问题在1.2.27版本中已经修复

# 版本升级建议
```
1.1.15~1.1.31 -> 1.1.31.sec01
1.1.32~1.1.33 -> 1.1.33.sec01 
1.1.34        -> 1.1.34.sec01
1.1.35~1.1.46 -> 1.1.46.sec01
1.2.0~1.2.2   -> 1.2.2.sec01 因为1.2.3之后的版本Map是没有排序输出的，如果不关注这个兼容问题，升级到1.2.26
1.2.3~1.2.7   -> 1.2.7.sec01 因为1.2.7使用最多特别提供，也可以直接使用1.2.8.sec01
1.2.8 -> 1.2.8.sec01
1.2.9~1.2.24 -> 1.2.29。
```
建议直接升级到1.2.28，如果遇到兼容问题在按照上面的对照表升级sec01版本。