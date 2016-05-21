在fastjson-1.2.12版本中，JSONField支持一个新的配置项jsonDirect，它的用途是：当你有一个字段是字符串类型，里面是json格式数据，你希望直接输入，而不是经过转义之后再输出。

### Model
```java
import com.alibaba.fastjson.annotation.JSONField;

public static class Model {
    public int id;
    @JSONField(jsonDirect=true)
    public String value;
}
```

### Usage
```java
Model model = new Model();
model.id = 1001;
model.value = "{}";

String json = JSON.toJSONString(model);
Assert.assertEquals("{\"id\":1001,\"value\":{}}", json);
```