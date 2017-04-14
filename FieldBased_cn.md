在1.2.31版本中，fastjson引入了对fieldBased序列化和反序列化的支持。在SerializeConfig和ParserConfig上配置是否fieldBased。

# Demo
```java
private static final boolean fieldBased = true;
private static SerializeConfig serializeConfig = new SerializeConfig(fieldBased);
private static ParserConfig parserConfig = new ParserConfig(fieldBased);

public static class Model {
    private int id;
}

Model model = new Model();
model.id = 123;
assertEquals("{\"id\":123}", JSON.toJSONString(model, serializeConfig));

Model model2 = JSON.parseObject("{\"id\":123}", Model.class, parserConfig);
assertEquals(model.id, model2.id);
```