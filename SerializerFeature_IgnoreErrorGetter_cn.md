在1.2.11版本之后，fastjson支持一个新的特性序列化特性IgnoreErrorGetter，用于忽略那些抛错的getter方法。使用方法如下：

```java
// 有一个会抛异常方法的JavaBean
public static class Model {
    private int id;
    public int getId() {
        return id;
    }
    public void setId(int id) {
        this.id = id;
    }
    public String getName() {
        throw new IllegalStateException(); // 抛异常
    }
}

// 测试代码
Model model = new Model();
model.setId(1001);
String text = JSON.toJSONString(model, SerializerFeature.IgnoreErrorGetter);
Assert.assertEquals("{\"id\":1001}", text);
```