在fastjson中，支持一种叫做BeanToArray的映射模式。普通模式下，JavaBean映射成json object，BeanToArray模式映射为json array。

### Sample 1
```
class Mode {
   public int id;
   public int name;
}

Model model = new Model();
model.id = 1001;
model.name = "gaotie";

String text_normal = JSON.toJSONString(model); // {"id":1001,"name":"gaotie"}
String text_beanToArray = JSON.toJSONString(model, SerializerFeature.BeanToArray); // [1001,"gaotie"]

JSON.parseObject(text_beanToArray, Feature.SupportArrayToBean); // support beanToArray & normal mode
```
上面的例子中，BeanToArray模式下，少了Key的输出，节省了空间，json字符串较小，性能也会更好。

### Sample 2
BeanToArray可以局部使用，比如：
```java
class Company {
     public int code;
     public List<Department> departments = new ArrayList<Department>();
}

@JSONType(serialzeFeatures=SerializerFeature.BeanToArray, parseFeatures=Feature.SupportArrayToBean))
class Department {
     public int id;
     public Stirng name;
     public Department() {}
     public Department(int id, String name) {this.id = id; this.name = name;}
}


Company company = new Company();
company.code = 100;
company.departments.add(new Department(1001, "Sales"));
company.departments.add(new Department(1002, "Financial"));

String text = JSON.toJSONString(commpany); // {"code":10,"departments":[[1001,"Sales"],[1002,"Financial"]]}
```
在这个例子中，如果Company的属性departments元素很多，局部采用BeanToArray就可以获得很好的性能，而整体又能够获得较好的可读性。
