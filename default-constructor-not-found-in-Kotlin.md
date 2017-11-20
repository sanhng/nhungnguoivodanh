I've got [this](https://github.com/alibaba/fastjson/wiki/Use-Fastjson-in-Kotlin)

## Data Class

```java
data class Configuration(val signature: String, val last_update: Long, val plugins: List<Plugins>)
```

## Try to serialize

```java
val configuration = JSON.parseObject(jsonString, Configuration::class.javaObjectType)
```

## Exception

```
com.alibaba.fastjson.JSONException: default constructor not found. class packagename.Configuration
   at com.alibaba.fastjson.parser.JavaBeanInfo.build(JavaBeanInfo.java:496)
   at com.alibaba.fastjson.parser.JavaBeanDeserializer.<init>(JavaBeanDeserializer.java:35)
   at com.alibaba.fastjson.parser.ParserConfig.getDeserializer(ParserConfig.java:225)
   at com.alibaba.fastjson.parser.ParserConfig.getDeserializer(ParserConfig.java:144)
   at com.alibaba.fastjson.parser.DefaultJSONParser.parseObject(DefaultJSONParser.java:683)
   at com.alibaba.fastjson.parser.DefaultJSONParser.parseObject(DefaultJSONParser.java:659)
   at com.alibaba.fastjson.JSON.parseObject(JSON.java:212)
   at com.alibaba.fastjson.JSON.parseObject(JSON.java:184)
   at com.alibaba.fastjson.JSON.parseObject(JSON.java:143)
   at com.alibaba.fastjson.JSON.parseObject(JSON.java:252)
   at packagename.Worker.run(Worker.kt:195)
   at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:422)
   at java.util.concurrent.FutureTask.run(FutureTask.java:237)
   at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1112)
   at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:587)
   at java.lang.Thread.run(Thread.java:841)
```

## Fastjson Version

1.1.64.android