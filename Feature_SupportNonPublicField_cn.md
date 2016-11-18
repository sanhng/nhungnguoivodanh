在某些场景下，反序列化需要支持NonPublicField，在1.2.22 & 1.1.54.android之后提供了相应的支持。

# Demo 1
```java
public class Model {
    private int id;
}

Model model = JSON.parseObject("{\"id\":123}", Model.class, Feature.SupportNonPublicField);
assertEquals(123, model.id);
```