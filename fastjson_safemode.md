## 打开SafeMode功能
在1.2.68之后的版本，在1.2.68版本中，fastjson增加了safeMode的支持。safeMode打开后，完全禁用autoType。

有三种方式配置SafeMode，如下:<br/>
### 1. 在代码中配置
```java
ParserConfig.getGlobalInstance().setSafeMode(true); 
```

### 2. 加上JVM启动参数
```script
    -Dfastjson.parser.safeMode=true 
```
如果有多个包名前缀，用逗号隔开

### 3. 通过fastjson.properties文件配置。
通过类路径的fastjson.properties文件来配置，配置方式如下：
```
fastjson.parser.safeMode=true
```