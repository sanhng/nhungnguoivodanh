# 1. JSONPath介绍
fastjson 1.2.0之后的版本支持JSONPath。

# 2. API
     package com.alibaba.fastjson;
     
     public class JSONPath {
          // 构造函数
          public JSONPath(String path) {} 
          // 求值方法
          public Object eval(Object rootObject) { }
     }

建议缓存JSONPath对象，这样能够提高求值的性能。

# 3. 支持语法
<table>
<tr><td>JSONPATH</td><td>描述</td></tr>
<tr><td>$</td><td>根对象</td></tr>
<tr><td>@</td><td>当前对象</td></tr>
<tr><td>[]</td><td>数组访问，例如$[0].leader.departments[1].name</td></tr>
<tr><td>.</td><td>属性访问，例如$.name</td></tr>
</table>

# 4. 示例

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
