```java
public static class Model {
    public int id;
    public String name;
}

Model model = new Model();

{
    DefaultJSONParser parser = new DefaultJSONParser("{\"id\":123,\"name\":\"wangsai-silence\"}");
    parser.parseObject(model);
    parser.close(); // 调用close能重用buf，提升性能

    assertEquals(123, model.id);
    assertEquals("wangsai-silence", model.name);
}

{
    DefaultJSONParser parser = new DefaultJSONParser("{\"id\":234,\"name\":\"wenshao\"}");
    parser.parseObject(model);
    parser.close(); // 调用close能重用buf，提升性能

    assertEquals(234, model.id);
    assertEquals("wenshao", model.name);
}
```