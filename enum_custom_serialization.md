fastjson支持在某些业务场景下，将Enum类型作为JavaBean序列化输出。
# 方法1
```java
public static class Model {
    public int id;
    public OrderType orderType;
}

public static enum OrderType implements JSONSerializable {
                              PayOrder(1, "支付订单"), //
                              SettleBill(2, "结算单");

    public final int    value;
    public final String remark;

    private OrderType(int value, String remark){
        this.value = value;
        this.remark = remark;
    }

    @Override
    public void write(JSONSerializer serializer, Object fieldName, Type fieldType,
                      int features) throws IOException {
        JSONObject json = new JSONObject();
        json.put("value", value);
        json.put("remark", remark);
        serializer.write(json);
    }

}
```

### 效果
```java
Model model = new Model();
model.id = 1001;
model.orderType = OrderType.PayOrder;
String text = JSON.toJSONString(model);
Assert.assertEquals("{\"id\":1001,\"orderType\":{\"remark\":\"支付订单\",\"value\":1}}", text);
```

# 方法2
使用@JSONType配置Enum当做JavaBean序列化，需要1.2.24之后的版本
```java
@JSONType(serializeEnumAsJavaBean = true)
public static enum OrderType {
    PayOrder(1, "支付订单"), //
    SettleBill(2, "结算单");

    public final int value;
    public final String remark;

    private OrderType(int value, String remark) {
        this.value = value;
        this.remark = remark;
    }
}
```

# 方法3
直接修改SerializeConfig配置Enum当做JavaBean序列化，需要1.2.24之后的版本，这个方法的好处是不需要修改Enum类的代码

```java
SerializeConfig serializeConfig = SerializeConfig.globalInstance;
serializeConfig.configEnumAsJavaBean(OrderType.class);
```
