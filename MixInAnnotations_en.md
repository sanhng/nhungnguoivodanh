# MixInAnnotations
1.2.60 added support for MixInAnnotations, with four brand new static APIs introduced in `JSON.class`. This feature is still under beta condition, feel free to have them tested. MixInAnnotations support configuring a MixIn class for a certain Target class and switching between different Target-MixIn combinations.

## 1. MixInAnnotations API
```Java
package com.alibaba.fastjson;

public abstract class JSON {
    // Associate Target class and MixIn class
    public static void addMixInAnnotations(Type target, Type mixIn)
    // Remove the association
    public static void removeMixInAnnotations(Type target)
    // Clear all associations
    public static void clearMixInAnnotations()
    // Get associated MixIn class for a given Target class
    public static Type getMixInAnnotations(Type target)
}
```
## 2. MixInAnnotations Use Case Example
Assuming we have a `Rectangle.class` that comes from a third-party library, whose definition is as followed:

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

This class might not serialize or deserialize in the way we expected, since:
- "w" and "h" seems hard to understand, better replaced by "width" and "height"
- getSize() may result in containing a non-exist field "size" in the output of serialization
- you can't add annotations directly to third-party classes in most cases

**Introducing MixInAnnotations：**

Define a MixIn class：
```Java
abstract class MixIn {
    @JSONField(name="width") abstract int getW(); // rename field
    @JSONField(name="height") abstract int getH(); // rename field
    @JSONField(serialize=false) abstract int getSize(); // go away, please
}
```
Use the APIs：
```Java
// Associate Target class and MixIn class
JSON.addMixInAnnotations(Rectangle.class, MixIn.class); 

// Serialization
Rectangle rectangle = new Rectangle(5, 10);
String str = JSON.toJSONString(rectangle);

System.out.println(str); // {"width":5, "height":10}

// Deserialization
Rectangle rectangle2 = JSON.parseObject(str, Rectangle.class);

System.out.println(rectangle2.getW()); // 5
System.out.println(rectangle2.getH()); // 10

// Remove association
JSON.removeMixInAnnotations(Rectangle.class)；
```

In addition, fastjson's MixInAnnotations supports switching between different MixIn classes:

```Java
abstract class MixIn_CN {
    @JSONField(name="长度") abstract int getW();
    @JSONField(name="宽度") abstract int getH();
    @JSONField(serialize=false) abstract int getSize();
}
```
Use case：
```Java
// Associate Target class and MixIn class
JSON.addMixInAnnotations(Rectangle.class, MixIn.class); 

// Serialization
Rectangle rectangle = new Rectangle(5, 10);
String str = JSON.toJSONString(rectangle);
System.out.println(str); // {"width":5, "height":10}

// Associate Target class and MixIn_CN class
JSON.addMixInAnnotations(Rectangle.class, MixIn_CN.class);

// Serialization
str = JSON.toJSONString(rectangle);
System.out.println(str); // {"宽度":5, "长度":10}

// Remove association
JSON.removeMixInAnnotations(Rectangle.class);

// Serialization
str = JSON.toJSONString(rectangle);
System.out.println(str); // {"h":10,"size":50,"w":5}
```

## 3. Usage notes
- MixInAnnotations support all annotation sets that fastjson recognizes, with the same usage migrates from Target class to MixIn class.
- A target class associates with the most recently associated MixIn class.
- Annotations for constructors from target class can directly be put on constructors with the same parameter types in MixIn class(even though they have different names)
- Make sure associated fields and methods(excepts constructors) in MixIn class have the same name and signature as those in Target class.
- MixInAnnotations work as expected within inheritance hierarchy.(For example, you can associate MixIn class to super-classes. In this case, the annotations will be overridden by annotations from sub-classes)
- It's not suggested to switch MixIn configuration for a single Target class under multi-threading environment.