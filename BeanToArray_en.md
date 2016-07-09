In fastjson, and supports a mapping mode, it is called BeanToArray. Normal mode, JavaBean mapped into json object, BeanToArray mode mapped to json array.

### Sample 1
```java
class Mode {
   public int id;
   public int name;
}

Model model = new Model();
model.id = 1001;
model.name = "gaotie";

// {"id":1001,"name":"gaotie"}
String text_normal = JSON.toJSONString(model); 

// [1001,"gaotie"]
String text_beanToArray = JSON.toJSONString(model, SerializerFeature.BeanToArray); 

// support beanToArray & normal mode
JSON.parseObject(text_beanToArray, Feature.SupportArrayToBean); 
```
he above example, under BeanToArray mode, less output Key, saving space, the smaller json string performance will be better.

### Sample 2
BeanToArray can be partially used, such as:
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

// {"code":10,"departments":[[1001,"Sales"],[1002,"Financial"]]}
String text = JSON.toJSONString(commpany); 
```
In this example, if the Company's departments attribute many of the elements, the use of local BeanToArray can get a good performance, but also to get a better overall readability.

# Performance
Use BeanToArray mode, you can get comparable performance protobuf.
```
                                   create     ser   deser   total   size  +dfl
protobuf                              244    2297    1296    3593    239   149
json/fastjson_array/databind          123    1289    1567    2856    281   163
msgpack/databind                      122    1525    2180    3705    233   146
json/fastjson/databind                120    2019    2610    4629    486   262
json/jackson+afterburner/databind     118    2142    3147    5289    485   261
json/jackson/databind                 124    2914    4411    7326    485   261
```
Here json / fastjson_array / databind is fastjson enabled BeanToArray mode, total performance is better than protobuf. Look here https://github.com/alibaba/fastjson/wiki/Benchmark_1_2_11