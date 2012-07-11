Use PropertyFilter
# Case 1
      import com.alibaba.fastjson.serializer.JSONSerializer;
      import com.alibaba.fastjson.serializer.PropertyFilter;
      import com.alibaba.fastjson.serializer.SerializeWriter;
       
      PropertyFilter filter = new PropertyFilter() {
          public boolean apply(Object source, String name, Object value) {
              return false;
          }
      };
 

      SerializeWriter out = new SerializeWriter();
      JSONSerializer serializer = new JSONSerializer(out);
      serializer.getPropertyFilters().add(filter);
       
      A a = new A();
      serializer.write(a);
 
      String text = out.toString();
      Assert.assertEquals("{}", text);

# Case 2
      PropertyFilter filter = new PropertyFilter() {
          public boolean apply(Object source, String name, Object value) {
              if("name".equals(name)) {
                  return true;
              }
              return false;
          }
      };
       
      SerializeWriter out = new SerializeWriter();
      JSONSerializer serializer = new JSONSerializer(out);
      serializer.getPropertyFilters().add(filter);
       
      A a = new A();
      a.setName("chennp2008");
      serializer.write(a);
       
      String text = out.toString();
      Assert.assertEquals("{\"name\":\"chennp2008\"}", text);

Entity

      public static class A {
          private int id;
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
