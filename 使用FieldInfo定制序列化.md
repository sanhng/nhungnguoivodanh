# JSONField 介绍
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

# JSONField配置方式
FieldInfo可以配置在getter/setter方法或者字段上。例如：
### 配置在getter/setter上

     public class A {
          private int id;
     
          @JSONField(name="ID")
          public int getId() {return id;}
          @JSONField(name="ID")
          public void setId(int value) {this.id = id;}
     }


### 配置在field上

     public class A {
          @JSONField(name="ID")
          private int id;
     
          public int getId() {return id;}
          public void setId(int value) {this.id = id;}
     }