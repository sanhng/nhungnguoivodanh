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


## PropertyPreFilter 根据PropertyName判断是否序列化

     public interface PropertyPreFilter extends SerializeFilter {
          boolean apply(JSONSerializer serializer, Object object, String name);
      }

