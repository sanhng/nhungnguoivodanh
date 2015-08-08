在Fastjson 1.2.7版本之后，fastjson提供LabelFilter功能，用于不同的场景定制序列化。

需要使用LabelFilter，首先需要用@JSONField配置label。如：

    public static class VO {
    
        private int    id;
        private String name;
        private String password;
        private String info;
    
        @JSONField(label = "normal")
        public int getId() {
            return id;
        }
    
        public void setId(int id) {
            this.id = id;
        }
    
        @JSONField(label = "normal")
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        @JSONField(label = "secret")
        public String getPassword() {
            return password;
        }
    
        public void setPassword(String password) {
            this.password = password;
        }
        
        public String getInfo() {
            return info;
        }
        
        public void setInfo(String info) {
            this.info = info;
        }
    }

根据不同场景过滤，如下：

    VO vo = new VO();
    vo.setId(123);
    vo.setName("wenshao");
    vo.setPassword("ooxxx");
    vo.setPassword("ooxxx");

    String text1 = JSON.toJSONString(vo, Labels.includes("normal"));
    Assert.assertEquals("{\"id\":123,\"name\":\"wenshao\"}", text1);

    String text2 = JSON.toJSONString(vo, Labels.excludes("secret"));
    Assert.assertEquals("{\"id\":123,\"info\":\"fofo\",\"name\":\"wenshao\"}", text2);
