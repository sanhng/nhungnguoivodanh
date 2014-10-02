FieldInfo可以配置在getter/setter方法或者字段上。例如：
### 配置在getter/setter上
{code}
public class A {
     private int id;

     @JSONField(name="ID")
     public int getId() {return id;}
     @JSONField(name="ID")
     public void setId(int value) {this.id = id;}
}
{code}

### 配置在field上
{code}
public class A {
     @JSONField(name="ID")
     private int id;

     public int getId() {return id;}
     public void setId(int value) {this.id = id;}
}
{code}