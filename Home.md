English | [中文] (https://github.com/AlibabaTech/fastjson/wiki/%E9%A6%96%E9%A1%B5)

# What is fastjson?
Fastjson is a JSON processor (JSON parser + JSON generator) written in Java:
* FAST (measured to be faster than any other Java parser and databinder, incudes jackson. )
* Powerful (full data binding for common JDK classes as well as any Java Bean class, Collection, Map, Date or enum)
* Zero-dependency (does not rely on other packages beyond JDK)
* Open Source (Apache License 2.0)

# Download
* Maven Central Repository : http://repo1.maven.org/maven2/com/alibaba/fastjson/
* Github Download : https://github.com/AlibabaTech/fastjson/downloads

# Maven dependency
    <dependency>
         <groupId>com.alibaba</groupId>
         <artifactId>fastjson</artifactId>
         <version>1.1.19</version>
    </dependency>

# Benchmark
Times are in nanoseconds, sizes are in bytes.

                                     create     ser   +same   deser   +shal   +deep   total   size  +dfl
    kryo                                119    1335    1273    1562    1709    1689    3024    223   140
    java-manual                         119    2129    2055    1005    1031    1062    3191    255   147
    json/fastjson/databind              117    1809    1687    1741    1786    1907    3715    486   262
    msgpack                             117    1827    1582    1985    2020    2118    3945    233   146
    json/jackson/manual                 118    1672    1501    2235    2232    2365    4037    468   253
    protobuf                            227    2939    1362    1626    1661    1965    4904    239   149
    thrift                              242    3157    2898    2031    2116    2194    5351    349   197
    json/jackson/databind               119    2851    2726    3941    4008    4154    7005    485   261
    hessian                             117    6135    5513   10082   10204   10311   16446    501   313
    json/google-gson/databind           117   11309   11304    7913    7967    8076   19385    486   259
    json/json-lib-databind              119   45547   45114  145951  145866  146582  192129    485   263

Columns: <br/>
* create: create an object (using the classes specified by the serialization tool)
* ser: create an object and serialize it
* +same: serialize the same object (i.e. doesn’t include creation time)
* deser: deserialize an object
* +shal: deserialize an object and access the top-level fields
* +deep: deserialize an object and access all the fields
* total: create + serialize + deserialize and access all fields
* size: the size of the serialized data
* +dfl: the size of the serialized data compressed with Java’s built-in implementation of DEFLATE (zlib)