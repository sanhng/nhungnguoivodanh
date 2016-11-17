# 配置JSONType.alphabetic属性
fastjson缺省时会使用字母序序列化，如果你是希望按照java fields/getters的自然顺序序列化，可以配置JSONType.alphabetic，使用方法如下：
```java
@JSONType(alphabetic = false)
public static class B {
    public int f2;
    public int f1;
    public int f0;
}
```