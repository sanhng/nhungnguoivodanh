fastjson序列化时，SerializeWriter会在ThreadLocal中持有一个buf，缺省最大是128K，在有些场景，需要序列化较大的json数据，可以将这个配置变大，提升性能。

# 支持版本
```
>= 1.2.52
```

# 配置方法
* JVM启动参数
```
-Dfastjson.serializer_buffer_threshold=256
```
* 配置fastjson.proerpties文件
```
fastjson.serializer_buffer_threshold=256
```