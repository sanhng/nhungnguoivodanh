在Fastjson 1.2.7版本之后，fastjson提供LabelFilter功能，用于不同的场景定制序列化。

需要使用LabelFilter，首先需要用@JSONField配置label。如：

    public static class VO {
    
        private int    id;
        private String name;
        private String password;
    
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
    

}