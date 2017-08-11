# Use Fastjson in Kotlin
In Kotlin, we use to make a data class to hold data, and then we can use Fastjson to serialize data-class object to json string or deserialize json string to data-class object now(Since Fastjson 1.2.37).There are three cases：

> note: in Kotlin, DataClassName::class.javaObjectType, equals javaObjectType.class in Java

## 1.Data Class without Any Annotation

Define DataClassSimple data-class:
```
data class DataClassSimple(val a : Int, val b : Int)
```

then, we can use this code below to serialize and deserialize:
```
    val dts = DataClassSimple(1,2)
    val jsons = JSON.toJSONString(dts)
    println(jsons)
    val clzs = DataClassSimple::class
    println(clzs.javaObjectType)
    val dt2 = JSON.parseObject(jsons,clzs.javaObjectType)
    println(dt2)
```

the output:
```
{"a":1,"b":2}
class DataClassSimple
DataClassSimple(a=1, b=2)
```

## 2.Data Class with @JSONField Annotation

Define DataClass data-class:
```
data class DataClass(@JSONField(name="aa")val a : Int, @JSONField(name="bb")val b : Int)
```

then we use JSON to serialize and deserialize:
```
    val dt = DataClass(1,2)
    val json = JSON.toJSONString(dt)
    println(json)
    val clz = DataClass::class
    println(clz.javaObjectType)
    val dt1 = JSON.parseObject(json,clz.javaObjectType)
    println(dt1)
```
the output:
```
{"aa":1,"bb":2}
class DataClass
DataClass(a=1, b=2)
```

## 3.Data Class with @field:JSONField Annotation

Define DataClassField data-class:
```
data class DataClassField(@field:JSONField(name="aaa")val a : Int, @field:JSONField(name="bbb")val b : Int)
```

then we use JSON to serialize and deserialize:
```
    val dtf = DataClassField(1,2)
    val jsonf = JSON.toJSONString(dtf)
    println(jsonf)
    val clzf = DataClassField::class
    println(clzf.javaObjectType)
    val dt3 = JSON.parseObject(jsonf,clzf.javaObjectType)
    println(dt3)
```
the output:
```
{"aaa":1,"bbb":2}
class DataClassField
DataClassField(a=1, b=2)
```