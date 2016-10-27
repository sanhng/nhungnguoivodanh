在fastjson中，支持一种叫做BeanToArray的映射模式。普通模式下，JavaBean映射成json object，BeanToArray模式映射为json array。

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
上面的例子中，BeanToArray模式下，少了Key的输出，节省了空间，json字符串较小，性能也会更好。

### Sample 2
BeanToArray可以局部使用，比如：
```java
class Company {
     public int code;
     public List<Department> departments = new ArrayList<Department>();
}

@JSONType(serialzeFeatures=SerializerFeature.BeanToArray, parseFeatures=Feature.SupportArrayToBean)
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
在这个例子中，如果Company的属性departments元素很多，局部采用BeanToArray就可以获得很好的性能，而整体又能够获得较好的可读性。

## Sample 3
上一个例子也可以这样写：
```java
class Company {
     public int code;

     @JSONField(serialzeFeatures=SerializerFeature.BeanToArray, parseFeatures=Feature.SupportArrayToBean)
     public List<Department> departments = new ArrayList<Department>();
}

```

# 性能
使用BeanToArray模式，可以获得媲美protobuf的性能。
```
                                   create     ser   deser   total   size  +dfl
protobuf                              244    2297    1296    3593    239   149
json/fastjson_array/databind          123    1289    1567    2856    281   163
msgpack/databind                      122    1525    2180    3705    233   146
json/fastjson/databind                120    2019    2610    4629    486   262
json/jackson+afterburner/databind     118    2142    3147    5289    485   261
json/jackson/databind                 124    2914    4411    7326    485   261
```
这里的json/fastjson_array/databind就是fastjson启用BeanToArray模式，total性能比protobuf好。具体看这里 https://github.com/alibaba/fastjson/wiki/Benchmark_1_2_11