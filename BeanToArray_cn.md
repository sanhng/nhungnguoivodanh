在fastjson中，支持一种叫做BeanToArray的映射模式。普通模式下，JavaBean映射成json object，BeanToArray模式映射为json array。

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

