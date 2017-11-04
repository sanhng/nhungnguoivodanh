# 1. 简介
fastjson缺省使用CamelCase，在1.2.15版本之后，fastjson支持配置PropertyNamingStrategy，支持如下四种:

name       | demo
-----------|-----------
CamelCase  | persionId
PascalCase | PersonId
SnakeCase  | person_id
KebabCase  | person-id

# 2. Serialization and Parser
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

# 3. 修改全局缺省的命名策略
```java
SerializeConfig.getGlobalInstance()
               .propertyNamingStrategy = PropertyNamingStrategy.PascalCase;
```

# 4. 基于JSONType配置PropertyNamingStrategy
```java
public void test_for_issue() throws Exception {
    Model model = new Model();
    model.userId = 1001;

    String text = JSON.toJSONString(model);

    assertEquals("{\"user_id\":1001}", text);

    Model model2 = JSON.parseObject(text, Model.class);
    assertEquals(1001, model2.userId);
}

@JSONType(naming = PropertyNamingStrategy.SnakeCase)
public static class Model {
    private int userId;

    public int getUserId() {
        return userId;
    }

    public void setUserId(int userId) {
        this.userId = userId;
    }
}
```