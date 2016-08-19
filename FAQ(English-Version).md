## 1. how to get fastjson?  
you can download fastjson:
* maven central repo: http://central.maven.org/maven2/com/alibaba/fastjson/  
* Sourceforge.net: https://sourceforge.net/projects/fastjson/files/  
* maven
the newest version of fastjson will be published to central maven repo, you can add the dependency.
```xml
<dependency>
     <groupId>com.alibaba</groupId>
     <artifactId>fastjson</artifactId>
     <version>1.2.12</version>
</dependency>
```
for android
```xml
<dependency>
     <groupId>com.alibaba</groupId>
     <artifactId>fastjson</artifactId>
     <version>1.1.52.android</version>
</dependency>
```
## 2. fastjson main API？
the entrance Class of fastjson is com.alibaba.fastjson.JSON，the main API are JSON.toJSONString and parseObject。
```java
package com.alibaba.fastjson;
public abstract class JSON {
      public static final String toJSONString(Object object);
      public static final <T> T parseObject(String text, Class<T> clazz, Feature... features);
}
```
serialize：
```java
String jsonString = JSON.toJSONString(obj);
```
deserialize：
```java
VO vo = JSON.parseObject("...", VO.class);
```
vector deserialize：
```java
import com.alibaba.fastjson.TypeReference;

List<VO> list = JSON.parseObject("...", new TypeReference<List<VO>>() {});
```
## 3. where can i find examples using fastjson
fastjson examples：https://github.com/alibaba/fastjson/wiki/Samples-DataBind

## 4. how about the performance of fastjson？
Until now, fastjson is the fastest json lib for Java, faster than the self-announced fastest jackson. The link is the third-party test result: https://github.com/eishay/jvm-serializers/wiki/Staging-Results 

When doing yourself testing, disable circular reference detect.
```java
JSON.toJSONString(obj, SerializerFeature.DisableCircularReferenceDetect)
VO vo = JSON.parseObject("...", VO.class, Feature.DisableCircularReferenceDetect)
```
Here is the comment about fastjon of the author of jackson cowtowncoder: 
https://groups.google.com/forum/#!topic/java-serialization-benchmarking/8eS1KOquAhw


## 5. fastjson v.s. gson?
fastjson is 6 times faster than gson, here is the testing result: https://github.com/eishay/jvm-serializers/wiki/Staging-Results 。gson的g可能是“龟”拼音的缩写，龟速的json库。

## 6. can fastjson be used in android?
fastjson has specific version for android, whose unusually function is removed. the size of jar is smaller. git branch address: https://github.com/alibaba/fastjson/tree/android

## 7. fastjson serialize is same with json-lib, who need to setting java ben serialize?
no, the only need is that the class is a java bean specification satisfied class.

## 8. how to do with date with fastjson?
so easy, for example:
```java
JSON.toJSONStringWithDateFormat(date, "yyyy-MM-dd HH:mm:ss.SSS")
```
with ISO-8601 date format
```java
JSON.toJSONString(obj, SerializerFeature.UseISO8601DateFormat);
```
global setting of date format
```java
JSON.DEFFAULT_DATE_FORMAT = "yyyy-MM-dd";
JSON.toJSONString(obj, SerializerFeature.WriteDateUseDateFormat);
```
auto recognize date format as below when deserialize:
* ISO-8601 format
* yyyy-MM-dd
* yyyy-MM-dd HH:mm:ss
* yyyy-MM-dd HH:mm:ss.SSS
* miliseconds
* miliseconds string
* .NET JSON format
* new Date(198293238)

## 9. 如何定制序列化？
你可以使用SimplePrePropertyFilter过滤字段，详细看这里：https://github.com/alibaba/fastjson/wiki/%E4%BD%BF%E7%94%A8SimplePropertyPreFilter%E8%BF%87%E6%BB%A4%E5%B1%9E%E6%80%A7

关于定制序列化，详细的介绍看这里：
https://github.com/alibaba/fastjson/wiki/%E5%AE%9A%E5%88%B6%E5%BA%8F%E5%88%97%E5%8C%96

## 10. 当对象存在引用时，序列化后的结果浏览器不支持，怎么办？
使用SerializerFeature.DisableCircularReferenceDetect特性关闭引用检测和生成。例如：
```java
String  jsonString = JSON.toJSONString(obj, SerializerFeature.DisableCircularReferenceDetect);
```
## 11. IE 6不支持JSON带中文字符串，要怎么处理？
fastjson提供了BrowserCompatible这个配置，打开之后，所有的中文都会序列化为\uXXXX这种格式，字节数会多一些，但是能兼容IE 6。
```java
String  jsonString = JSON.toJSONString(obj, SerializerFeature.BrowserCompatible);
```
## 12. fastjson 如何处理超大对象和超大JSON文本
fastjson提供了Stream API，详细看这里 https://github.com/alibaba/fastjson/wiki/Stream-api

## 13. 使用@JSONField定制序列化
fastjson提供了使用Annotation定制序列化和反序列化的功能。https://github.com/alibaba/fastjson/wiki/JSONField
