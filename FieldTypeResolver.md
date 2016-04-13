FieldTypeResolver是1.2.9 & 1.1.49.android中引入的新功能，用于解析嵌套对象时，自动识别子对象的类型信息。FieldTypeResolver只会作用于value类型为json object的字段。自动识别类型，能避免二次解析，使用起来更简单，性能也会更好。

例如：

```java
public static class Item {
    public int value;
}

FieldTypeResolver fieldResolver = new FieldTypeResolver() {
    public Type resolve(Object object, String fieldName) {
        if (fieldName.startsWith("item_")) { // 字段名称为item_开始的对象，识别类型为Item
            return Item.class;
        }
        
        return null;
    }
};

String text = "{\"item_0\":{},\"item_1\":{},\"item_2\":1001}";
JSONObject o = JSON.parseObject(text, JSONObject.class, fieldResolver);
Assert.assertTrue(o.get("item_0") instanceof Item);
Assert.assertTrue(o.get("item_1") instanceof Item);
Assert.assertTrue(o.get("item_2") instanceof Integer); // 类型还是Integer，因为value是Integer，而不是Object。
```
例子中可以看出，item_2的value没有被FieldTypeResolver影响，类型还是Integer，因为value是Integer，而不是Object。