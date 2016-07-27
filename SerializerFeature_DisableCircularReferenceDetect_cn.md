在fastjson中，会自动检测循环引用，并且输出为fastjson专有的引用表示格式。但这个不能被其他JSON库识别，也不能被浏览器识别，所以fastjson提供了关闭循环引用检测的功能。使用如下：
```java
import com.alibaba.fastjson.serializer.SerializerFeature;

JSON.toJSONString(obj, SerializerFeature.DisableCircularReferenceDetect);
```