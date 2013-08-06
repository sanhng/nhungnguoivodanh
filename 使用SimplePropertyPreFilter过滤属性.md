需要根据不同的环境返回定制化返回属性时，可以使用SimplePropertyPreFilter。

# SimplePropertyPreFilter接口
SimplePropertyPreFilter的代码接口如下：
      
      public class SimplePropertyPreFilter implements PropertyPreFilter {      
          public SimplePropertyPreFilter(String... properties){
              this(null, properties);
          }
      
          public SimplePropertyPreFilter(Class<?> clazz, String... properties){
              ... ...
          }
      
          public Class<?> getClazz() {
              return clazz;
          }
      
          public Set<String> getIncludes();
      
          public Set<String> getExcludes();
      ...
      }

你可以配置includes、excludes。当clazz不为null时，针对特定类型；当class为null时，针对所有类型。

当includes的size > 0时，属性必须在includes中才会被序列化，excludes优先于includes。

# 使用介绍
在1.1.23版本之后，JSON提供新的序列化接口toJSONString，如下：
      
      String toJSONString(Object, SerializeFilter, SerializerFeature...);
      

使用方式如下：
      
      VO vo = new VO();
      
      vo.setId(123);
      vo.setName("flym");
      
      SimplePropertyPreFilter filter = new SimplePropertyPreFilter(VO.class, "name");
      Assert.assertEquals("{\"name\":\"flym\"}", JSON.toJSONString(vo, filter));
      
      public static class VO {
          private int    id;
          private String name;
      
          public int getId() {
              return id;
          }
          public void setId(int id) {
              this.id = id;
          }

          public String getName() {
              return name;
          }
          public void setName(String name) {
              this.name = name;
          }
      }
      