Fastjson is a Java library that can be used to convert Java Objects into their JSON representation. It can also be used to convert a JSON string to an equivalent Java object. Fastjson can work with arbitrary Java objects including pre-existing objects that you do not have source-code of.

### Fastjson Goals
 * Provide best performance in server side and android client.
 * Provide simple toJSONString() and parseObject() methods to convert Java objects to JSON and vice-versa
 * Allow pre-existing unmodifiable objects to be converted to and from JSON
 * Extensive support of Java Generics
 * Allow custom representations for objects
 * Support arbitrarily complex objects (with deep inheritance hierarchies and extensive use of generic types)

### Using Fastjson
```java
import com.alibaba.fastjson.JSON;

// 
Model model = new Model();
String json = JSON.toJSONString(obj); // encode obj to json

Model model2 = JSON.parseObject(json, Model.class); // parse json string to java bean

// parse json to list with generic type.
TypeReference<List<Model>> typeRef = new TypeReference<List<Model>>() {};
List<Model> modelList = JSON.parseObject(json, typeRef); 

```