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
SerializeConfig.globalInstance.configEnumAsJavaBean(OrderType.class);
```

# 方法4
在fastjson 1.2.71版本之后，支持配置JSONField或者MixIn的方法做定制序列化和反序列化
```java
public void test_for_issue() throws Exception {
    VO vo = new VO();
    vo.type = Color.Black;

    String str = JSON.toJSONString(vo);
    assertEquals("{\"type\":1003}", str);

    VO vo2 = JSON.parseObject(str, VO.class);

}

public static class VO {
    public Color type;
}

public enum Color {
    Red(1001),
    White(1002),
    Black(1003),
    Blue(1004);

    private final int code;

    private Color(int code) {
        this.code = code;
    }

    @JSONField
    public int getCode() {
        return code;
    }

    @JSONCreator
    public static Color from(int code) {
        for (Color v : values()) {
            if (v.code == code) {
                return v;
            }
        }

        throw new IllegalArgumentException("code " + code);
    }
}
```

# 方法5
在fastjson 1.2.71版本之后，支持配置JSONField或者MixIn的方法做定制序列化和反序列化
```java
public void test_for_issue() throws Exception {
    JSON.addMixInAnnotations(Color.class, ColorMixedIn.class);

    VO vo = new VO();
    vo.type = Color.Black;

    String str = JSON.toJSONString(vo);
    assertEquals("{\"type\":1003}", str);

    VO vo2 = JSON.parseObject(str, VO.class);
}

public static class VO {
    public Color type;
}

public enum Color {
    Red(1001),
    White(1002),
    Black(1003),
    Blue(1004);

    private final int code;

    private Color(int code) {
        this.code = code;
    }

    public int getCode() {
        return code;
    }

    public static Color from(int code) {
        for (Color v : values()) {
            if (v.code == code) {
                return v;
            }
        }

        throw new IllegalArgumentException("code " + code);
    }
}

public static class ColorMixedIn {
    @JSONField
    public int getCode() {
        return 0;
    }

    @JSONCreator
    public static Color from(int code) {
        return null;
    }
}
```


