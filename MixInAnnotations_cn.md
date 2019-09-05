# MixInAnnotations
1.2.60新增加对MixInAnnotations注解方式的支持，在JSON类中提供4个新的静态API，还在验证阶段，欢迎试用。支持为指定类进行MixIn类的配置，以及在不同MixIn配置间进行切换。

## 1. MixInAnnotations API
```Java
package com.alibaba.fastjson;

public abstract class JSON {
    // 关联Target类与MixIn类
    public static void addMixInAnnotations(Type target, Type mixIn)
    // 移除Target类的MixIn关联关系
    public static void removeMixInAnnotations(Type target)
    // 清除所有MixIn关联关系
    public static void clearMixInAnnotations()
    // 获取与Target类关联的MixIn类
    public static Type getMixInAnnotations(Type target)
}
```
## 2. MixInAnnotations使用场景示例
假设现有的第三方类源码Rectangle.class定义如下

```Java
public final class Rectangle {
    final private int w, h;
    public Rectangle(int w, int h) {
      this.w = w;
      this.h = h;
    }
    public int getW() { return w; }
    public int getH() { return h; }
    public int getSize() { return w * h; }
}
```

这个类序列化和反序列化的结果可能并不理想，因为：
- "w"和"h"属性名似乎不太好理解，换为"width"和"height"会更好些
- getSize()方法会导致序列化出的结果中包含"size"这个不存在的属性
- 第三方类无法直接在源码中添加注解

**通过MixInAnnotations解决问题：**

MixIn类定义：
```Java
abstract class MixIn {
    @JSONField(name="width") abstract int getW(); // 重命名属性
    @JSONField(name="height") abstract int getH(); // 重命名属性
    @JSONField(serialize=false) abstract int getSize(); // 不序列化的属性
}
```
API使用：
```Java
//关联Target类与MixIn类
JSON.addMixInAnnotations(Rectangle.class, MixIn.class); 

// 序列化
Rectangle rectangle = new Rectangle(5, 10);
String str = JSON.toJSONString(rectangle);

System.out.println(str); // {"width":5, "height":10}

//反序列化
Rectangle rectangle2 = JSON.parseObject(str, Rectangle.class);

System.out.println(rectangle2.getW()); // 5
System.out.println(rectangle2.getH()); // 10

//移除关联
JSON.removeMixInAnnotations(Rectangle.class)；
```

除此之外，MixInAnnotations还支持配置的切换：

```Java
abstract class MixIn_CN {
    @JSONField(name="长度") abstract int getW(); // 重命名属性
    @JSONField(name="宽度") abstract int getH(); // 重命名属性
    @JSONField(serialize=false) abstract int getSize(); // 不序列化的属性
}
```
使用场景：
```Java
//关联Target类与MixIn类
JSON.addMixInAnnotations(Rectangle.class, MixIn.class); 

// 序列化
Rectangle rectangle = new Rectangle(5, 10);
String str = JSON.toJSONString(rectangle);
System.out.println(str); // {"width":5, "height":10}

//关联Target类与MixIn_CN类
JSON.addMixInAnnotations(Rectangle.class, MixIn_CN.class);

// 序列化
str = JSON.toJSONString(rectangle);
System.out.println(str); // {"宽度":5, "长度":10}

//移除Target类的关联关系
JSON.removeMixInAnnotations(Rectangle.class);

// 序列化
str = JSON.toJSONString(rectangle);
System.out.println(str); // {"h":10,"size":50,"w":5}
```

## 3. 使用事项
- MixInAnnotations支持原fastjson中所有注解的使用场景，Target类上的注解可原封不动地移植到MixIn类上并保持相同行为。
- 一个Target类只与最近配置的MixIn类关联
- Target类构造方法上的注解可直接移植到MixIn类的同参不同名构造方法上
- Target类与MixIn类的属性及方法通过名字与签名进行关联（构造方法可以不同名）
- MixInAnnotations支持类继承结构，（例如可以将MixIn类配置给父类，此时子类的注解会将父类的覆盖）
- 不建议在多线程环境下对同一个Target类进行配置切换