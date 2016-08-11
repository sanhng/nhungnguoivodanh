# 1. JSONField 介绍

    package com.alibaba.fastjson.annotation;
    
    public @interface JSONField {
        // 配置序列化和反序列化的顺序，1.1.42版本之后才支持
        int ordinal() default 0;
    
         // 指定字段的名称
        String name() default "";
    
        // 指定字段的格式，对日期格式有用
        String format() default "";
    
        // 是否序列化
        boolean serialize() default true;
    
        // 是否反序列化
        boolean deserialize() default true;
    }

# 2. JSONField配置方式
FieldInfo可以配置在getter/setter方法或者字段上。例如：
## 2.1 配置在getter/setter上

     public class A {
          private int id;
     
          @JSONField(name="ID")
          public int getId() {return id;}
          @JSONField(name="ID")
          public void setId(int value) {this.id = id;}
     }


## 2.2 配置在field上

     public class A {
          @JSONField(name="ID")
          private int id;
     
          public int getId() {return id;}
          public void setId(int value) {this.id = id;}
     }

# 3. 使用format配置日期格式化

     public class A {
          // 配置date序列化和反序列使用yyyyMMdd日期格式
          @JSONField(format="yyyyMMdd")
          public Date date;
     }

# 4. 使用serialize/deserialize指定字段不序列化

     public class A {
          @JSONField(serialize=false)
          public Date date;
     }

     public class A {
          @JSONField(deserialize=false)
          public Date date;
     }

# 5. 使用ordinal指定字段的顺序
缺省fastjson序列化一个java bean，是根据fieldName的字母序进行序列化的，你可以通过ordinal指定字段的顺序。这个特性需要1.1.42以上版本。

    public static class VO {
        @JSONField(ordinal = 3)
        private int f0;

        @JSONField(ordinal = 2)
        private int f1;

        @JSONField(ordinal = 1)
        private int f2;
    }

# 6. 使用serializeUsing制定属性的序列化类
在fastjson 1.2.16版本之后，JSONField支持新的定制化配置serializeUsing，可以单独对某一个类的某个属性定制序列化，比如：
```java
public static class Model {
    @JSONField(serializeUsing = ModelValueSerializer.class)
    public int value;
}

public static class ModelValueSerializer implements ObjectSerializer {
    @Override
    public void write(JSONSerializer serializer, Object object, Object fieldName, Type fieldType,
                      int features) throws IOException {
        Integer value = (Integer) object;
        String text = value + "元";
        serializer.write(text);
    }
}
```

测试代码
```
Model model = new Model();
model.value = 100;
String json = JSON.toJSONString(model);
Assert.assertEquals("{\"value\":\"100元\"}", json);
```



