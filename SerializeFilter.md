# 简介
SerializeFilter是通过编程扩展的方式定制序列化。fastjson支持6种SerializeFilter，用于不同场景的定制序列化。

1. PropertyPreFilter 根据PropertyName判断是否序列化
2. PropertyFilter 根据PropertyName和PropertyValue来判断是否序列化
3. NameFilter 修改Key，如果需要修改Key,process返回值则可
4. ValueFilter 修改Value
5. BeforeFilter 序列化时在最前添加内容
6. AfterFilter 序列化时在最后添加内容

# PropertyFilter 根据PropertyName和PropertyValue来判断是否序列化

      public interface PropertyFilter extends SerializeFilter {
          boolean apply(Object object, String propertyName, Object propertyValue);
      }

可以通过扩展实现根据object或者属性名称或者属性值进行判断是否需要序列化。例如：

        PropertyFilter filter = new PropertyFilter() {

            public boolean apply(Object source, String name, Object value) {
                if ("id".equals(name)) {
                    int id = ((Integer) value).intValue();
                    return id >= 100;
                }
                return false;
            }
        };
        
        JSON.toJSONString(obj, filter); // 序列化的时候传入filter


# PropertyPreFilter 根据PropertyName判断是否序列化
和PropertyFilter不同只根据object和name进行判断，在调用getter之前，这样避免了getter调用可能存在的异常。

     public interface PropertyPreFilter extends SerializeFilter {
          boolean apply(JSONSerializer serializer, Object object, String name);
      }


# NameFilter 序列化时修改Key
如果需要修改Key,process返回值则可
```java
public interface NameFilter extends SerializeFilter {
    String process(Object object, String propertyName, Object propertyValue);
}
```

fastjson内置一个PascalNameFilter，用于输出将首字符大写的Pascal风格。
例如：
```
import com.alibaba.fastjson.serializer.PascalNameFilter;

Object obj = ...;
String jsonStr = JSON.toJSONString(obj, new PascalNameFilter());
```

# ValueFilter 序列化是修改Value

      public interface ValueFilter extends SerializeFilter {
          Object process(Object object, String propertyName, Object propertyValue);
      }

# BeforeFilter 在序列化对象的所有属性之前执行某些操作,例如调用 writeKeyValue 添加内容

      public abstract class BeforeFilter implements SerializeFilter {
          protected final void writeKeyValue(String key, Object value) { ... }
          // 需要实现的抽象方法，在实现中调用writeKeyValue添加内容
          public abstract void writeBefore(Object object);
      }

# AfterFilter 在序列化对象的所有属性之后执行某些操作,例如调用 writeKeyValue 添加内容

      public abstract class AfterFilter implements SerializeFilter {
          protected final void writeKeyValue(String key, Object value) { ... }
          // 需要实现的抽象方法，在实现中调用writeKeyValue添加内容
          public abstract void writeAfter(Object object);
      }