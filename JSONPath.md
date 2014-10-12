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
<tr><td>[?(@.key)]</td><td>对象属性非空过滤，例如$.departs[?(@.name)]</td></tr>
<tr><td>[?(@.key > 123)]</td><td>数值对象属性，例如$.departs[?(@.id >= 123)]，比较操作符支持=,!=,>,>=,&lt;,&lt;= </td></tr>
<tr><td>length() 或者 size()</td><td>数组长度。例如$.values.size()，支持类型java.util.Map和java.util.Collection和数组</td></tr>
<tr><td>.</td><td>属性访问，例如$.name</td></tr>
<tr><td>*</td><td>对象的所有属性，例如$.leader.*</td></tr>
<tr><td>['key']</td><td>属性访问。例如$['name']</td></tr>
<tr><td>['key0','key1']</td><td>多个属性访问。例如$['id','name']</td></tr>
</table>

以下两种写法的语义是相同的：

    $.store.book[0].title
和

    $['store']['book'][0]['title']


# 4. 语法示例
<table>
<tr><td>JSONPath</td><td>语义</td></tr>
<tr><td>$</td><td>根对象</td></tr>
<tr><td>$[-1]</td><td>最后元素</td></tr>
<tr><td>$[:-2]</td><td>第1个至倒数第2个</td></tr>
<tr><td>$[1:]</td><td>第2个之后所有元素</td></tr>
<tr><td>$[1,2,3]</td><td>集合中1,2,3个元素</td></tr>
</td>
</table>

# 5. API 示例

    public void test_entity() throws Exception {
        // 在实际使用中，建议缓存path对象，避免重复创建，这样性能更好
        JSONPath path = new JSONPath("$.value"); 

        Entity entity = new Entity();
        entity.setValue(new Object());
        Assert.assertSame(entity.getValue(), path.eval(entity));
    }
    
    public static class Entity {
        private Object value;
        public Object getValue() { return value; }
        public void setValue(Object value) { this.value = value; }
    }
