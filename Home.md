English | [中文](https://github.com/Alibaba/fastjson/wiki/%E9%A6%96%E9%A1%B5)

Fastjson is a Java library that can be used to convert Java Objects into their JSON representation. It can also be used to convert a JSON string to an equivalent Java object. Fastjson can work with arbitrary Java objects including pre-existing objects that you do not have source-code of.

### Fastjson Goals
 * Provide [best performance](https://github.com/alibaba/fastjson/wiki/Benchmark_1_2_11) in server side and android client.
 * Provide simple toJSONString() and parseObject() methods to convert Java objects to JSON and vice-versa.
 * Allow pre-existing unmodifiable objects to be converted to and from JSON.
 * Extensive support of Java Generics.
 * Allow custom representations for objects.
 * Support arbitrarily complex objects (with deep inheritance hierarchies and extensive use of generic types).

# Frequently Asked Questions
https://github.com/alibaba/fastjson/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98

# Download
### android developer plz see [Here][0]

[the latest JAR][1] 

or via Maven:
```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>VERSION_CODE</version>
</dependency>
```

or via Gradle:
```groovy
compile 'com.alibaba:fastjson:VERSION_CODE'
```

replace `VERSION_CODE` with real version name such as `1.2.21` released in [Here][2] or [Here][3] or [Here][4].

[0]: https://github.com/alibaba/fastjson/wiki/Android%E7%89%88%E6%9C%AC
[1]: https://search.maven.org/remote_content?g=com.alibaba&a=fastjson&v=LATEST
[2]: http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.alibaba%22%20AND%20a%3A%22fastjson%22
[3]: http://repo1.maven.org/maven2/com/alibaba/fastjson/
[4]: https://bintray.com/bintray/jcenter/com.alibaba%3Afastjson#files

# Getting started
Samples : https://github.com/alibaba/fastjson/wiki/Samples-DataBind

# Google JSON Style Guide
you can learn how to write JSON gracefully from here：https://google.github.io/styleguide/jsoncstyleguide.xml

# Integrate Fastjson in Spring
https://github.com/alibaba/fastjson/wiki/%E5%9C%A8-Spring-%E4%B8%AD%E9%9B%86%E6%88%90-Fastjson

# Integrate Fastjson in JAX-RS
https://github.com/alibaba/fastjson/wiki/Integrate-Fastjson-in-JAXRS

# Use Fastjson in Kotlin
https://github.com/alibaba/fastjson/wiki/Use-Fastjson-in-Kotlin