这个功能参考自jackson。 POJO的Builder通过@JSONType来配置，如下：

````
VO vo = JSON.parseObject("{\"id\":12304,\"name\":\"ljw\"}", VO.class);
        
Assert.assertEquals(12304, vo.getId());
Assert.assertEquals("ljw", vo.getName());
````

````
@JSONType(builder=VOBuilder.class)
public static class VO {
    private int id;
    private String name;
        
    public int getId() {
        return id;
    }
        
    public String getName() {
        return name;
    }
}

// 如果builder方法是build或者create，能自动识别
@JSONPOJOBuilder(buildMethod="xxx")
public static class VOBuilder {

    private VO vo = new VO();

    public VO xxx() {
        return vo;
    }
        
    public VOBuilder withId(int id) {
        vo.id = id;
        return this;
    }
        
    public VOBuilder withName(String name) {
        vo.name = name;
        return this;
    }
}
````