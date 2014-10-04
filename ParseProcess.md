# 1. 简介
ParseProcess是编程扩展定制反序列化的接口。fastjson支持如下ParseProcess：

* ExtraProcessor 用于处理多余的字段
* ExtraTypeProvider 用于处理多余字段时提供类型信息

# 2. 使用ExtraProcessor 处理多余字段

    public static class VO {
        private int                 id;
        private Map<String, Object> attributes = new HashMap<String, Object>();
        public int getId() { return id; }
        public void setId(int id) { this.id = id;}
        public Map<String, Object> getAttributes() { return attributes;}
    }
        
    ExtraProcessor processor = new ExtraProcessor() {
        public void processExtra(Object object, String key, Object value) {
            VO vo = (VO) object;
            vo.getAttributes().put(key, value);
        }
    };
        
    VO vo = JSON.parseObject("{\"id\":123,\"name\":\"abc\"}", VO.class, processor);
    Assert.assertEquals(123, vo.getId());
    Assert.assertEquals("abc", vo.getAttributes().get("name"));

# 3. 使用ExtraTypeProvider 为多余的字段提供类型

    public static class VO {
        private int                 id;
        private Map<String, Object> attributes = new HashMap<String, Object>();
        public int getId() { return id; }
        public void setId(int id) { this.id = id;}
        public Map<String, Object> getAttributes() { return attributes;}
    }
        
    class MyExtraProcessor implements ExtraProcessor, ExtraTypeProvider {
        public void processExtra(Object object, String key, Object value) {
            VO vo = (VO) object;
            vo.getAttributes().put(key, value);
        }
        
        public Type getExtraType(Object object, String key) {
            if ("value".equals(key)) {
                return int.class;
            }
            return null;
        }
    };
    ExtraProcessor processor = new MyExtraProcessor();
        
    VO vo = JSON.parseObject("{\"id\":123,\"value\":\"123456\"}", VO.class, processor);
    Assert.assertEquals(123, vo.getId());
    Assert.assertEquals(123456, vo.getAttributes().get("value"));
