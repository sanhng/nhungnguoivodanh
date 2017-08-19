由于历史原因，fastjson的getter/setter提取属性名没有完全按照JavaBean规范，为了兼容旧版本，一直没有修改。但是可以配置遵循JavaBean规范。

## 配置JVM启动参数
```
-Dfastjson.compatibleWithJavaBean=true
```

## 调用API设置
```java
com.alibaba.fastjson.util.TypeUtils.compatibleWithJavaBean = true;
```