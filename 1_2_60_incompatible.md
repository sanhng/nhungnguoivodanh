## 问题1
1.2.57后版本，会识别下划线后缀的名字，比如"id_"，如果需要精确匹配使用Feature.DisableFieldSmartMatch。比如：    ​ 
```java   ​
​VO3 vo = JSON.parseObject(text, VO3.class, Feature.DisableFieldSmartMatch);
```

## 问题2
1.2.57后版本，toJavaObject或JSONObject.getObject方法，如果传入JSONObject.class，会报错，比如：
```java
List<JSONObject> json = JSON.parseArray("[{\"values\":[{}]}]", JSONObject.class);
for (JSONObject obj : json) {
    obj.getObject("values", new TypeReference<List<JSONObject>>() {});  // 这里不支持JSONObject
}
```