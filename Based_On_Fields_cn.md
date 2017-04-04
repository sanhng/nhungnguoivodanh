在1.2.31版本开始，支持based on fields序列化和反序列化，使用方式如下：

```java
SerializeConfig config = new SerializeConfig(true); // singleton
ParserConfig parserConfig = new ParserConfig(true); // singleton

public static class Model {
    private int id;
}

Model model = new Model();
model.id = 123;
assertEquals("{\"id\":123}", JSON.toJSONString(model, config));

Model model2 = JSON.parseObject("{\"id\":123}", Model.class, parserConfig);
assertEquals(model.id, model2.id);
```