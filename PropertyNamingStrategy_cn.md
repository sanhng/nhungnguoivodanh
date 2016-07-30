fastjson缺省使用CamelCase，在1.2.15版本之后，fastjson支持配置PropertyNamingStrategy，支持如下四种:

name       | demo
-----------|-----------
CamelCase  | persionId
PascalCase | PersonId
SnakeCase  | person_id
KebabCase  | person-id

# Serialization and Parser
```java
SerializeConfig config = new SerializeConfig(); // 生产环境中，config要做singleton处理，要不然会存在性能问题
config.propertyNamingStrategy = PropertyNamingStrategy.SnakeCase;

Model model = new Model();
model.personId = 1001;
String text = JSON.toJSONString(model, config);
Assert.assertEquals("{\"person_id\":1001}", text);

ParserConfig parserConfig = new ParserConfig(); // 生产环境中，parserConfig要做singleton处理，要不然会存在性能问题
parserConfig.propertyNamingStrategy = PropertyNamingStrategy.SnakeCase;
Model model2 = JSON.parseObject(text, Model.class, parserConfig);
Assert.assertEquals(model.personId, model2.personId);
```