# 1. JSONPath介绍
fastjson 1.2.0之后的版本支持JSONPath。


# 2. 例子

    public void test_entity() throws Exception {
        Entity entity = new Entity();
        entity.setValue(new Object());
        Assert.assertSame(entity.getValue(), new JSONPath("$.value").eval(entity));
    }
    
    public static class Entity {
        private Object value;
        public Object getValue() { return value; }
        public void setValue(Object value) { this.value = value; }
    }
