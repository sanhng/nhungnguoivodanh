在某些场景中，序列化希望按父类的字段信息，不包括子类的字段。在1.2.57中提供了支持。比如：
```java
public class Issue2289 extends TestCase {
    public void test_for_issue() throws Exception {
        B b = new B();
        b.id = 123;

        JSONSerializer jsonSerializer = new JSONSerializer();
        jsonSerializer.writeAs(b, A.class); // 按父类序列化

        String str = jsonSerializer.toString();
        assertEquals("{}", str);
    }

    public static class A {

    }

    public static class B extends A {
        public int id;
    }
}
```