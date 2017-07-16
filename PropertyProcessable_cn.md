这是一个新增的自定义反序列化接口。
```java
interface PropertyProcessable {
    // 返回property的类型，如果返回空，则由parser自行推断。
    Type getType(String name);

    // 处理属性值
    void apply(String name, Object value);
}
```

```java
public static class VO implements PropertyProcessable {
    public int id;
    public String name;
    public Value value;

    public Type getType(String name) {
        if ("value".equals(name)) {
            return Value.class;
        }
        return null;
    }

    public void apply(String name, Object value) {
        if ("vo_id".equals(name)) {
            this.id = ((Integer) value).intValue();
        } else if ("vo_name".equals(name)) {
            this.name = (String) value;
        } else if ("value".equals(name)) {
            this.value = (Value) value;
        }
    }
}

public static class Value {

}

///////////// 使用
VO vo = JSON.parseObject("{\"vo_id\":123,\"vo_name\":\"abc\",\"value\":{}}", VO.class);
assertEquals(123, vo.id);
assertEquals("abc", vo.name);
assertNotNull(vo.value);
```