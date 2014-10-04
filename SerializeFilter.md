SerializeFilter是通过编程扩展的方式定制序列化。fastjson支持6种SerializeFilter，用于不同场景的定制序列化。

1. PropertyPreFilter 根据PropertyName判断是否序列化
2. PropertyFilter 根据PropertyName和PropertyValue来判断是否序列化
3. NameFilter 修改Key，如果需要修改Key,process返回值则可
4. ValueFilter 修改Value
5. BeforeFilter 序列化时在最前添加内容
6. AfterFilter 序列化时在最后添加内容

## PropertyFilter 根据PropertyName和PropertyValue来判断是否序列化

      public interface PropertyFilter extends SerializeFilter {
          boolean apply(Object object, String propertyName, Object propertyValue);
      }

## PropertyPreFilter 根据PropertyName判断是否序列化

     public interface PropertyPreFilter extends SerializeFilter {
          boolean apply(JSONSerializer serializer, Object object, String name);
      }