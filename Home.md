Fastjson is a JSON processor (JSON parser + JSON generator) written in Java:
* FAST (measured to be faster than any other Java parser and databinder, incudes jackson. )
* Powerful (full data binding for common JDK classes as well as any Java Bean class, Collection, Map, Date or enum)
* Zero-dependency (does not rely on other packages beyond JDK)
* Open Source (Apache License 2.0)

# Maven dependency
    <dependency>
         <groupId>com.alibaba</groupId>
         <artifactId>fastjson</artifactId>
         <version>1.1.18</version>
    </dependency>

# Benchmark
Times are in nanoseconds, sizes are in bytes.

                                     create     ser   +same   deser   +shal   +deep   total   size  +dfl
    java-manual                         121    2134    2049    1010    1036    1106    3240    255   147
    hessian                             120    6208    5681    9310    9477    9616   15824    501   313
    kryo                                122    1353    1283    1625    1643    1722    3074    223   140
    protobuf                            241    2902    1396    1622    1690    1953    4854    239   149
    thrift                              251    3236    2987    2057    2124    2153    5389    349   197
    msgpack                             123    1874    1609    1990    2048    2020    3893    233   146
    json/jackson/manual                 122    1588    1502    2186    2252    2299    3886    468   253
    json/jackson/databind               123    2745    2619    4234    4325    4486    7231    485   261
    json/fastjson/databind              122    1841    1698    1608    1672    1730    3571    486   262

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