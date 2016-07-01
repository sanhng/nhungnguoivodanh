在1.2.14版本之后，fastjson支持通过JSONType配置定制序列化的ObjectSerializer。使用如下
```java
@JSONType(serializer=ModelSerializer.class)
public static class Model {
    public int id;
}

public static class ModelSerializer implements ObjectSerializer {

    @Override
    public void write(JSONSerializer serializer, Object object, Object fieldName, Type fieldType,
                      int features) throws IOException {
        Model model = (Model) object;
        SerializeWriter out = serializer.getWriter();
        out.writeFieldValue('{', "ID", model.id);
        out.write('}');
    }
    
}
```

使用
```java
Model model = new Model();
model.id = 1001;
String text = JSON.toJSONString(model);
Assert.assertEquals("{\"ID\":1001}", text);
```