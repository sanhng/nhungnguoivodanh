在fastjson-1.2.11中，序列化性能有了很大提升，反序列化性能也有所提升，所以做一次和其他序列化库的性能对比测试。

# 测试场景
采用各个序列化库作者都比较认可的一个测试，来自 https://github.com/eishay/jvm-serializers ，由于官方的测试还没采用最新版本的fastjson，所以我fork修改使用最新的api，代码在这里 https://github.com/wenshao/jvm-serializers/tree/fastjson-1.2.11

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
```
{"images":[{"height":768,"size":"LARGE","title":"Javaone Keynote","uri":"http://javaone.com/keynote_large.jpg","width":1024},{"height":240,"size":"SMALL","title":"Javaone Keynote","uri":"http://javaone.com/keynote_small.jpg","width":320}],"media":{"bitrate":262144,"duration":18000000,"format":"video/mpg4","height":480,"persons":["Bill Gates","Steve Jobs"],"player":"JAVA","size":58982400,"title":"Javaone Keynote","uri":"http://javaone.com/keynote.mpg","width":640}}
```

# 测试结果