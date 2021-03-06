大多数json是用于程序的读写，有时候，为了可读性，需要对json格式化输出，fastjson提供了一个序列化特性 SerializerFeature.PrettyFormat

# demo
### 代码
```java
public  static class Model {
    public int id;
    public String name;
}

Model model = new Model();
model.id = 123;
model.name = "wenshao";
String text = JSON.toJSONString(model, SerializerFeature.PrettyFormat);
assertEquals("{\n" +
        "\t\"id\":123,\n" +
        "\t\"name\":\"wenshao\"\n" +
        "}", text);
```

### 输出
输出的text如下
```json
{
	"id":123,
	"name":"wenshao"
}
```

# 另外一种写法
在JSON中提供了一个写法，早期没有SerializerFeature.PrettyFormat的写法，一直保留着。如下：
```
public static String toJSONString(Object object, boolean prettyFormat) {
    if (!prettyFormat) {
        return toJSONString(object);
    }

    return toJSONString(object, SerializerFeature.PrettyFormat);
}
```