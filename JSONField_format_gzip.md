在1.2.33版本中，JSONField.format增加了对gzip压缩的支持，当用json传输较大的byte[]时可以启用减少网络传输。
## Demo
```java
public static class Model {
    @JSONField(format = "gzip")
    public byte[] value;
}

Model model = new Model();

StringBuffer buf = new StringBuffer();
for (int i = 0; i < 1000; ++i) {
    buf.append("0123456890");
    buf.append("ABCDEFGHIJ");
}

model.value = buf.toString().getBytes();

String json = JSON.toJSONString(model);

assertEquals("{\"value\":\"H4sIAAAAAAAAAO3IsRGAIBAAsJVeUE5LBBXcfyC3sErKxJLyupX9iHq2ft3PmG8455xzzjnnnHPOOeecc84555xzzjnnnHPOOeecc84555xzzjnnnHPOOeecc84555z7/T6powiAIE4AAA==\"}", json);

Model model1 = JSON.parseObject(json, Model.class);
Assert.assertArrayEquals(model.value, model1.value);
```