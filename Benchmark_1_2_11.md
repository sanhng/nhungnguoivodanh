在fastjson-1.2.11中，序列化性能有了很大提升，反序列化性能也有所提升，所以做一次和其他序列化库的性能对比测试。

# 测试场景
采用各个序列化库作者都比较认可的一个测试，来自 https://github.com/eishay/jvm-serializers ，由于官方的测试还没采用最新版本的fastjson，所以我fork修改使用最新的api，代码在这里 https://github.com/wenshao/jvm-serializers/tree/fastjson-1.2.11

### 运行测试
```
git clone https://github.com/wenshao/jvm-serializers.git
cd jvm-serializers/tpc
make
./run-bench.sh json/jackson+afterburner/databind,json/fastjson/databind,json/fastjson_array/databind,protobuf,json/jackson/databind,msgpack/databind
```
### 类结构
eishay的场景，有三个类，类结构如下
```java
class MediaContent {
	public Media media;
	public Image[] images;
}
class Media implements java.io.Serializable {
    public enum Player { JAVA, FLASH }
    public String       uri;
    public String       title;     // Can be unset.
    public int          width;
    public int          height;
    public String       format;
    public long         duration;
    public long         size;
    public boolean      hasBitrate;
    public List<String> persons;
    public Player       player;
    public String       copyright; // Can be unset.
}

class Image {
    public enum Size { SMALL, LARGE }
    public String uri;
    public String title; // Can be null
    public int    width;
    public int    height;
    public Size   size;
}
```
详细代码看这里：
* https://github.com/wenshao/jvm-serializers/blob/fastjson-1.2.11/tpc/src/data/media/MediaContent.java
* https://github.com/wenshao/jvm-serializers/blob/fastjson-1.2.11/tpc/src/data/media/Media.java
* https://github.com/wenshao/jvm-serializers/blob/fastjson-1.2.11/tpc/src/data/media/Image.java

### 测试数据
测试的场景是[media.1.cks](https://github.com/wenshao/jvm-serializers/blob/fastjson-1.2.11/tpc/data/media.1.cks)，对应的json如下
```json
{"images":[{"height":768,"size":"LARGE","title":"Javaone Keynote","uri":"http://javaone.com/keynote_large.jpg","width":1024},{"height":240,"size":"SMALL","title":"Javaone Keynote","uri":"http://javaone.com/keynote_small.jpg","width":320}],"media":{"bitrate":262144,"duration":18000000,"format":"video/mpg4","height":480,"persons":["Bill Gates","Steve Jobs"],"player":"JAVA","size":58982400,"title":"Javaone Keynote","uri":"http://javaone.com/keynote.mpg","width":640}}
```

fastjson中，如果启用BeanToArray模式，对应的json为：
```
[[[768,1,"Javaone Keynote","http://javaone.com/keynote_large.jpg",1024],[240,0,"Javaone Keynote","http://javaone.com/keynote_small.jpg",320]],[262144,null,18000000,"video/mpg4",480,["Bill Gates","Steve Jobs"],0,58982400,"Javaone Keynote","http://javaone.com/keynote.mpg",640]]
```

### 参与测试各个库的版本
```
fastjson-1.2.11
jackson-2.7.0
protobuf-java-2.3.0.jar
```

# 测试结果
### 阿里云新加坡主机，普通配置，1核1024M内存
```
                                   create     ser   deser   total   size  +dfl
json/fastjson_array/databind          123    1289    1567    2856    281   163
json/fastjson/databind                120    2019    2610    4629    486   262
json/jackson+afterburner/databind     118    2142    3147    5289    485   261
json/jackson/databind                 124    2914    4411    7326    485   261
msgpack/databind                      122    1525    2180    3705    233   146
protobuf                              244    2297    1296    3593    239   149

```

### Raspberry Pi 3
```
                                   create     ser   deser   total   size  +dfl
json/fastjson_array/databind          961   18162   19106   37268    281   163
json/fastjson/databind                976   31240   29890   61129    486   262
json/jackson+afterburner/databind     975   24539   34337   58876    485   261
json/jackson/databind                 979   28238   49380   77618    485   261
msgpack/databind                     1027   18768   26617   45385    233   146
protobuf                             2626   26095   12538   38633    239   149
```