在fastjson-1.2.11中，序列化性能有了很大提升，反序列化性能也有所提升，所以做一次和其他序列化库的性能对比测试。

### 测试场景
采用各个序列化库作者都比较认可的一个测试，来自 https://github.com/eishay/jvm-serializers ，由于官方的测试还没采用最新版本的fastjson，所以我fork修改使用最新的api，代码在这里 https://github.com/wenshao/jvm-serializers/tree/fastjson-1.2.11
