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
<tr><td>[num]</td><td>数组访问，其中num是数字，可以是负数。例如$[0].leader.departments[-1].name</td></tr>
<tr><td>[num0,num1,num2...]</td><td>数组多个元素访问，其中num是数字，可以是负数，返回数组中的多个元素。例如$[0,3,-2,5]</td></tr>
<tr><td>[start:end]</td><td>数组范围访问，其中start和end是开始小表和结束下标，可以是负数，返回数组中的多个元素。例如$[0:5]</td></tr>
<tr><td>[start:end :step]</td><td>数组范围访问，其中start和end是开始小表和结束下标，可以是负数；step是步长，返回数组中的多个元素。例如$[0:5:2]</td></tr>
<tr><td>.</td><td>属性访问，例如$.name</td></tr>
<tr><td>*</td><td>对象的所有属性，例如$.leader.*</td></tr>
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
