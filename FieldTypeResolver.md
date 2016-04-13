FieldTypeResolver是1.2.9 & 1.1.49.android中引入的新功能，用于解析嵌套对象时，自动识别子对象的类型信息。

例如：

```java
public static class Item {
    public int value;
}

FieldTypeResolver fieldResolver = new FieldTypeResolver() {
    public Type resolve(Object object, String fieldName) {
        if (fieldName.startsWith("item_")) {
            return Item.class;
        }
        
        return null;
    }
};

String text = "{\"item_0\":{\"value\":1001},\"item_1\":{\"value\":1002}}";
JSONObject jsonObject = JSON.parseObject(text, JSONObject.class, fieldResolver);
Assert.assertTrue(jsonObject.get("item_0") instanceof Item);
Assert.assertTrue(jsonObject.get("item_1") instanceof Item);
```