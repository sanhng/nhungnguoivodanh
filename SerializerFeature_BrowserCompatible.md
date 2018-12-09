在JavaScript中，整数必须在-9007199254740991~9007199254740991之间，如果超过这个范围，会被阶段。为了绕开这个限制，在对客户端输出整数可能超出这个范围时，使用SerializerFeature.BrowserCompatible。

## 1. 直接使用SerializerFeature.BrowserCompatible
```java
String str = JSON.toJSONString(obj, SerializerFeature.BrowserCompatible);
```

## 2. 全局手工配置
```java
JSON.DEFAULT_GENERATE_FEATURE |= SerializerFeature.QuoteFieldNames.getMask();
```