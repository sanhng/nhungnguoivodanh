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
        model.userName = "test";
        String text = JSON.toJSONString(model);
        assertEquals("{\"userName\":\"test\",\"user_id\":1001}", text);

        Model model2 = JSON.parseObject(text, Model.class);

        assertEquals(1001, model2.userId);
        assertEquals("test", model2.userName);
    }

    /**
     * 当某个字段有JSONField注解，JSONField中name属性不存在，并且类上有属性转换策略，json属性名也要用类上的属性名转换策略为为准
     * @throws Exception
     */
    public void test_when_JSONField_have_not_name_attr() throws Exception {
        ModelTwo modelTwo = new ModelTwo();
        modelTwo.userId = 1001;
        modelTwo.userName = "test";
        String text = JSON.toJSONString(modelTwo);
        assertEquals("{\"userName\":\"test\",\"user_id\":\"1001\"}", text);

        Model model2 = JSON.parseObject(text, Model.class);

        assertEquals(1001, model2.userId);
        assertEquals("test", model2.userName);
    }

    @JSONType(naming = PropertyNamingStrategy.SnakeCase)
    public static class Model {
        private int userId;
        @JSONField(name = "userName")
        private String userName;

        public int getUserId() {
            return userId;
        }

        public void setUserId(int userId) {
            this.userId = userId;
        }

        public String getUserName() {
            return userName;
        }

        public void setUserName(String userName) {
            this.userName = userName;
        }
    }

    @JSONType(naming = PropertyNamingStrategy.SnakeCase)
    public static class ModelTwo {
        /**
         * 此字段准备序列化为字符串类型
         */
        @JSONField(serializeUsing = StringSerializer.class)
        private int userId;
        @JSONField(name = "userName")
        private String userName;

        public int getUserId() {
            return userId;
        }

        public void setUserId(int userId) {
            this.userId = userId;
        }

        public String getUserName() {
            return userName;
        }

        public void setUserName(String userName) {
            this.userName = userName;
        }
    }
```