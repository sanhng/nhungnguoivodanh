这是一个新增的自定义反序列化接口。
```java
interface PropertyProcessable {
    // 返回property的类型，如果返回空，则由parser自行推断。
    Type getType(String name);

    // 处理属性值
    void apply(String name, Object value);
}
```